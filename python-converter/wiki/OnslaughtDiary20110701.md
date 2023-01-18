## 1st July 2011

![Dave Jeffery's cool title screen, and something to read while it loads...](../../retrosoftwarecouk_wiki-20160918-wikidump/images/blurploader.png "fig:Dave Jeffery's cool title screen, and something to read while it loads...") I decided it was time for another diversion, and to think about the title screen and loading sequence.

I wanted to be able to credit everyone who was involved with the creation of Blurp, from my one-time Beeb collaborator, Matt Godbolt, to all those from this community who have contributed so much. I don't have the memory to do this as a scrolltext or something in-game, so the obvious thing seemed to be to create an intro section, with the title screen and a message.

Rather than a scrolling message, I decided I'd prefer page-by-page text, which I can fade in and out smoothly with palette changes. This has the advantage of being rather quicker to render, which means I can put it into an interrupt routine. _This_ means that it can be left to run in the background while I do something else - for example, loading!

I've always been keen to give Blurp a very polished look - to the same quality of presentation as one of Orlando's games, for example. So this meant that even the loading process had to look nice! The first thing I decided to do was scrap the Acorn font, and use the standard Sega arcade font, just because it looks a little bit different - somehow, more like an arcade game!

Thinking first of the tape release, I also decided I'd like to use my turbo loader routine which I [demoed a little while ago](http://www.retrosoftware.co.uk/forum/viewtopic.php?p=4693#p4693). Along with the interrupt-driven message, this really takes the tedium out of tape loading, and the whole thing (including title screen) actually loads in around 3 minutes!

Anyway, I thought I'd use this blog entry to talk a little bit about the turbo loader, and how it came about in the first place. 'Turbo' is actually something of a misnomer, because the loading speed is no different from normal - still 1200 baud, as this is the fastest that the Beeb tape hardware can go. Instead, I employ two tricks in order to try and get the fastest performance out of the loader:

- The data is stored on tape as one continuous block, with no header. The inter-block gaps and repeated block headers in regular Beeb tape files really slow the loading down. If the Ultimate games can load as one continuous block, so can Blurp!

- The data is a [LZ77](http://en.wikipedia.org/wiki/LZ77) compressed bitstream, which is decompressed at load time. Typically my algorithm compresses to 60-65% of the original size, which immediately saves a huge amount of time.

The LZ77 decompression algorithm is very simple, which is why it's possible to do it in real time, while the tape loads. In simple terms, it goes something like this:

1.  Set an output pointer to the start address of memory to load into.

2.  Read the next item from the tape. It may be one of two types - literal data or reference data.

    - If it's literal data, just write it straight out to the output pointer and advance it.

    - If it's reference data, then this represents a repetition of a block of data already written out, and so consists of two parts - the start address of the repeated block (actually an offset from the current pointer), and the length of the block - so copy the block to the current ouput pointer, and advance it accordingly.

3.  Go back to 2, and repeat until we run out of data.

A nice thing about LZ77 compression is that it implements run-length encoding for free. Suppose you need to encode a block of 10 zeroes. With LZ77, you would write one zero as a literal, and then write a reference block with an offset of -1, and a length of 9. As long as the block is copied ascending in memory (from the first address to the last), the newly copied bytes are themselves copied further up the block in subsequent iterations. This also allows more cunning run-length encodings, such as repeated pairs of bytes, e.g. &55 &AA &55 &AA &55 &AA (write &55 &AA as literals, and then a reference block with offset -2 and length 4).

It's really very very simple. The 'art' is in the implementation, or how you actually store the data in the bitstream. Naively, you could say:

- 1 bit - 0 = literal, 1 = reference

- If literal : 8 bits = literal

- If reference : 12 bits = offset, 8 bits = length

But, imagine an uncompressable data block, where everything is encoded as a literal. The extra 1 bit overhead (to denote each item as a 'literal') would add 12% more to the length of the data when 'compressed'. This is too much.

I was inspired by an app, well known in the C64 world, called [pucrunch](http://www.cs.tut.fi/~albert/Dev/pucrunch/), which performs a very efficient implementation of LZ77 compression. I decided to see if I could do better, and create sometihng with a smaller runtime code footprint, and a better average compression ratio.

Pucrunch does some crazy things with escape bits in order to minimise the need to mark data as literal or reference. I decided to opt for something much more simple. The first item will _always_ be a literal (as there is not yet any data to reference). In fact, it's more than likely that, for a little while, everything will be a literal. So we store a count of the number of literals which follow, and then store the block of literals as an array of 8-bit data. After this, we know it has to be a reference item, so for simplicity, why not take the same approach - store a count of the number of reference items which follow, and then the block of reference items themselves. Hence we toggle between reading blocks of literals and blocks of reference data, which makes the decompression code very simple.

Looking at compressed data, it turns out that this is quite a good scheme. Not only are literals often evident in contiguous blocks, but so is reference data, particularly in graphics. By using an [Elias gamma code](http://en.wikipedia.org/wiki/Elias_gamma_coding) to store the 'count', we even minimise the storage for the other common case which is where there is just one item of reference data amongst a block of literals (as the value 1 is represented by just a single bit).

In the end, it turns out that I usually get marginally better compression ratios than pucrunch - but occasionally it performs better. It really is very, very good! But for the smaller run-time code footprint, I'm happy to stick with my scheme.

_[&lt;&lt; Previous entry](OnslaughtDiary20110604 "wikilink")_

_[Home](OnslaughtDiary "wikilink")_

---

### Comments

- (Example comment to demonstrate markup).

  - [Richtw](User%3ARichtw "wikilink") 09:23, 1 July 2011 (BST)
