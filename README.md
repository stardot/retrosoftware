# retrosoftware.co.uk

Contents from the retrosoftware.co.uk site

This is a full export of the MediaWiki site from 18-09-2016.

## Aims

It would be great if we could convert the `XML` content to the Github wiki format.

If anyone has time, and PHP installed, perhaps they could take a look at: https://github.com/philipashlock/mediawiki-to-markdown

Alternatively, if there's a way to convert the WikiMedia content to a HTML site that would be a great option too, since we could host it using Github pages.

Another option - https://github.com/peterjc/mediawiki_to_git_md

Which is a python solution, that I tried to have a quick go at - https://github.com/stardot/retrosoftware.co.uk/tree/master/python-converter

The results are workable, but a lot of html/edge cases need weeding out - see the sample output here: https://github.com/stardot/retrosoftware.co.uk/tree/master/python-converter/wiki

## Github Pages hosting

Supposing we just want to preserve the content, then maybe the best bet is to get a 'good enough' markdown conversion of each page from the original site before it went offline, and then we can hand tweak each file over time to make them render ok.

Once that is done (or even while we do it), a simple Jekyll template in this repo would allow the site to be preserved and accessed as a website in its static 'archived' state.
