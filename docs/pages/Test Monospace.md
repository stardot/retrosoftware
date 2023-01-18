# Examples of writing up mono-spaced and pre-formatted text on the wiki

### Using the &lt;code&gt; tag, &nbsp; and &lt;br/&gt; tags

Surround the text with &lt;code&gt; or &lt;tt&gt; tags (they're synonymous), use HTML line breaks &lt;br/&gt; at the end of lines, and use the HTML code for a non-breaking space &nbsp; to represent spaces. Both wikitext markup (e.g. apostrophes used for italics/bold) and special HTML characters, like &gt; are interpreted. Recommended for true mono-space requirements.

*Please remember that, as wikitext will still be interpreted within the &lt;code&gt; tag, you should check the page output carefully to ensure that nothing has been unintentionally interpreted by the wiki. If anything has, you should surround the appropriate text with a &lt;nowiki&gt; tag.*

<span style="font-variant:small-caps">Wikitext code:</span>

`<code>`
`<span` `style="color:#008000">\` `Simple` `example` `illustrating` `use` `of` `monospacing</span><br/>`
`lll` `;` `&nbsp;&nbsp;&nbsp;` `an` `''italic''` `comment` `&gt;` `by` `<span` `style="color:#0000C0">Blue` `Person</span><br/>`
`AAA` `;` `&nbsp;&nbsp;&nbsp;` `followed` `by` `a` `'''bold'''` `comment` `&gt;` `by` `<span` `style="color:#C00000">Red` `Person</span>`
`</code>`

<span style="font-variant:small-caps">Output:</span>

<span style="color:#008000">`\` `Simple` `example` `illustrating` `use` `of` `monospacing`</span>
`lll` `;` `   ` `an` *`italic`* `comment` `>` `by` <span style="color:#0000C0">`Blue` `Person`</span>
`AAA` `;` `   ` `followed` `by` `a` **`bold`** `comment` `>` `by` <span style="color:#C00000">`Red` `Person`</span>

### Using a single space to start each line

Use a single space at the start of each line, to pre-format the text, in a separate box. Both wikitext markup (e.g. apostrophes used for italics/bold) and special HTML characters, like &gt; are interpreted. Not true mono-spacing.

<span style="font-variant:small-caps">Wikitext code:</span>

` <span` `style="color:#008000">\` `Simple` `example` `illustrating` `use` `of` `a` `single` `space` `at` `the` `start` `of` `lines</span>`
` lll` `;` `   ` `an` `''italic''` `comment` `&gt;` `by` `<span` `style="color:#0000C0">Blue` `Person</span>`
` AAA` `;` `   ` `followed` `by` `a` `'''bold'''` `comment` `&gt;` `by` `<span` `style="color:#C00000">Red` `Person</span>`

<span style="font-variant:small-caps">Output:</span>

<span style="color:#008000">`\ Simple example illustrating use of a single space at the start of lines`</span>
`lll ;     an `*`italic`*` comment > by `<span style="color:#0000C0">`Blue Person`</span>
`AAA ;     followed by a `**`bold`**` comment > by `<span style="color:#C00000">`Red Person`</span>

### Using the &lt;pre&gt; tag

Similar output to using a single space at the start of each line, use the &lt;pre&gt; tag to surround a block of text you want pre-formatted, in a separate box but, unlike using a single-space at the start of each line, wikitext markup (e.g. apostrophes used for italics/bold or span colouring) is **not** interpreted. Special HTML characters, like &gt; are still interpreted, however. Not true mono-spacing.

<span style="font-variant:small-caps">Wikitext code:</span>

`<pre>`
`<span` `style="color:#008000">\` `Simple` `example` `illustrating` `use` `of` `pre-formatted` `text</span>`
`lll` `;` `   ` `an` `''italic''` `comment` `&gt;` `by` `<span` `style="color:#0000C0">Blue` `Person</span>`
`AAA` `;` `   ` `followed` `by` `a` `'''bold'''` `comment` `&gt;` `by` `<span` `style="color:#C00000">Red` `Person</span>`
`</pre>`

<span style="font-variant:small-caps">Output:</span>

    <span style="color:#008000">\ Simple example illustrating use of pre-formatted text</span>
    lll ;     an ''italic'' comment &gt; by <span style="color:#0000C0">Blue Person</span>
    AAA ;     followed by a '''bold''' comment &gt; by <span style="color:#C00000">Red Person</span>
