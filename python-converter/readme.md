Conversion process.

Recommend installing Python 2.7.9 (which includes pip)
https://www.python.org/downloads/release/python-279/

A good idea to make sure latest pip is installed:
pip install --upgrade setuptools pip
Will probably need to pip install requests also

---


Use dumpwiki pythonscript to scrape the online wiki from (http://www.retrosoftware.co.uk/wiki/index.php)

Clone the repo from https://github.com/WikiTeam/wikiteam
run the following:
dumpgenerator.py http://www.retrosoftware.co.uk/wiki/ --xml --images





---

Now we can convert the XML dump to github GFM wiki repo
Create a new repo, and clone the git repo for the Wiki part.
https://help.github.com/articles/adding-and-editing-wiki-pages-locally/


---

Install pandoc
https://github.com/jgm/pandoc/releases/tag/1.17.2

---

Convert the XML dumpfile

Run the conversion script convert.py to covert the XML dumpfile to a GFM wiki repo
This script is a modified version of https://github.com/peterjc/mediawiki_to_git_md

