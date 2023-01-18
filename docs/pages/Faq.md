# Retro Software Frequently Asked Questions (FAQ)

### One question. The platform is 30 years old. Why?!

Acorn's OS 1.2 still boots faster than any major commercial operating system available today. :)

### I've logged in, why can't I edit the wiki/post to the forum?

This site is an amalgamation of a MediaWiki wiki, phpBB3 forums and Mantis bug tracker. There are two sets of accounts - those for the forums/wiki and those for the bug tracker. However, the account integration between the wiki and forums is not entirely seamless - you must log into both the wiki and the forums separately, if you wish to use them both. Similarly, logging out of the forums will not log you out of the wiki, and vice versa.

Assuming you're a regular contributor, we suggest you create a forum account and then login to both the forum and the wiki, letting your web browser remember the credentials. That way, you'll remain permanently logged in and won't have to worry about it. :)

If you need to report a bug, you can then sign up to the Bug Tracker when required.

### How do I get started in this community?

If you're a volunteer who simply wants to assist wherever you can; please register your willingness to help by creating a new thread within the [Retro Software Volunteer Team](http://www.retrosoftware.co.uk/forum/viewforum.php?f=23) forum (all projects will require testing at least, but feel free to list your skills).

On the other hand, if you've joined us with a project already in mind, you could start by posting some information about it to the [I'm thinking of programming ...](http://www.retrosoftware.co.uk/forum/viewforum.php?f=19) forum. That will get some interest. At which point, if you request it, our Retro Software Helping Hands can create you a forum for users to discuss your project, a new project within our bug tracker, to help keep track of bugs/feature requests, and also provide a template for a wiki page, where you can post information, updates and news on the project's progress - you can edit it, so you can list anything project-related that you want! You can also post requests for assistance - you'll find there are a number of volunteers willing to help with platform and gameplay testing, background music, and lots of other things you may find useful. Just ask!

When your project finally reaches fruition, you can then decide how to release it. If you just want to provide a free disk image for anyone to download, you can host that here. However, if you'd like to release an actual cassette tape or disk for use with an original microcomputer, you may find our community can help with production, distribution and the design of packaging & cover artwork.

### How do I get started programming for the BBC Micro?

The BBC Micro itself provides a simple language for writing programs called BBC BASIC, and you can get started with it using an emulator like [BeebEm](http://www.mkw.me.uk/beebem/) and the original [BBC Microcomputer User Guide](http://www.retrosoftware.co.uk/wiki/index.php/UsefulDocs#User_Guides). The BBC Micro also has a built-in assembler which can be used to write 6502 machine code - this is more complex than writing a typical BASIC program but it allows you much greater control over the machine and can run significantly faster. If you want to jump straight into assembler, you can browse the resources on the [Useful Docs](UsefulDocs "wikilink") page and then start by downloading the SWIFT IDE from the [Dev Tools](DevelopmentTools "wikilink") page. The SWIFT page contains a number of video tutorials and the IDE provides the game [Sparse Invaders](Sparse_Invaders "wikilink") as a sample project to help you get started. Of course, feel free to post any questions you may have in the [Programming Discussion](http://www.retrosoftware.co.uk/forum/viewforum.php?f=11) forum.

### Why isn't my forum post/wiki entry picked up by the search function?

This site is an amalgamation of MediaWiki and phpbb3. The search functions have not been combined, though, so there are two separate search functions. The wiki search function in the top right corner is replaced with the forum search function, when you browse to the forums. To search the whole site, you will need to run your search with both search functions.

### How can I upload a non-picture file such as a disk image to the wiki?

In the interests of encouraging people to keep the size of their uploaded files to a minimum, we've restricted the uploads to images and Zip archives. You should zip the disk image etc. before uploading it. If you have a valid reason for wanting to upload an uncompressed file, then raise it with the site administrators via the [Retro Software Feedback](http://www.retrosoftware.co.uk/forum/viewforum.php?f=3) forum.

### What is the largest file I can upload to the wiki?

The maximum size of files that can be uploaded is 30 MB.

### Can I embed a flash-based video from one of the popular video sharing services, into a wiki page?

You can embed videos into any page with either of the following source snippets:

-   `{{#ev:service|id}}` -or-
-   `{{#ev:service|id|width}}`

Where:

-   `service` is the name of a video sharing service - `dailymotion`, `funnyordie`, `googlevideo`, `sevenload`, `revver`, `vimeo` or `youtube`.
-   `id` is the id of the video to include
-   `width` (optional) is the width in pixels of the viewing area (height will be determined automatically)

At the time of writing, YouTube videos are limited to 320 by 240 pixels and a bitrate of around 314kbit/s by re-encoding the uploaded video at the time of upload. Uploaded videos are also limited to 10 minutes and 1 GB. Google Video's Help Center, on the other hand, claims that videos can be uploaded "without any size or length limitations" so that might be an alternative if your video is particularly large and/or long.

### Can I embed a flash-based video from one of the popular video sharing services, into the forum?

You can embed videos into a forum post using the `[flash]` tag:

-   YouTube: `[flash=425,350]http://www.youtube.com/v/id&fmt=22[/flash]`
-   Google Video: `[flash=425,350]http://video.google.com/googleplayer.swf?docId=id[/flash]`
-   Dailymotion: `[flash=425,350]http://www.dailymotion.com/swf/id[/flash]`
-   Funny or Die: `[flash=425,350]http://www.funnyordie.com/v1/flvideo/fodplayer.swf?file=http://funnyordie.vo.llnwd.net/o16/id.flv&autoStart=false[/flash]`
-   sevenload: `[flash=425,350]http://page.sevenload.com/swf/en_GB/player.swf?id=id[/flash]`
-   Revver: `[flash=425,350]http://flash.revver.com/player/1.0/player.swf?mediaId=id[/flash]`

Where:

-   `id` is the id of the video to include
-   `425` is the width in pixels of the viewing area
-   `350` is the height in pixels of the viewing area

### How can I create a video review of Retro Software games like the ones I've seen on YouTube?

We have a wiki tutorial on just that topic, [How To: Create BeebEm Video Reviews](HowToCreateBeebEmVideoReviews "wikilink").

### How can I format code snippets on the wiki so they are displayed in a monospace-spaced font?

This isn't quite as easy to achieve as we might hope, but you can use the &lt;code&gt; tag, &nbsp; and &lt;br/&gt; tags to achieve monospacing. Complete examples of some options are available on the [Test Monospace](Test_Monospace "wikilink") page.


