Generic Directives is still in active discussion in http://talk.commonmark.org/t/generic-directives-plugins-syntax . But for brainstorming purposes, here is some possible extensions to support, or at least adhere to if not included. 

It might look like `!extensionName[](){}` for inline

and for block (Current talk page at http://talk.commonmark.org/t/block-directives/802 )

    !!!extentionNames: argumentField { #id .class key1=value key2=value }
    ...BlockContent...
    !!!

-------

Below is a list of extensions and it's purpose. 

* **extensionName** : 
 * Purpose: 
 * [] : contentField 
 * () : argumentField 
 * {} : keyValueField 

* **** : 
 * Purpose: 
 * [] :  
 * () :  
 * {} :  

-----------

* **default** : default extension
 * Purpose: used if no extension name is specified. Reads url, and chooses the appropriate extensions. E.g. .png will be embedded using the `image` extension
 * [] : 
 * () : Reads the url name to determine filetype
 * {} : 

* **image** : embed image
 * Purpose: embeds image in page
 * [] : image alt text
 * () : image url
 * {} : width="width of image", height="height of image"

* **`extensionName`.help** : display documentation
 * Purpose: displays documentations on how to use the extension
 * [] : 
 * () : 
 * {} : shortVersion=True/False

* **`extensionName`.settings** : 
 * Purpose: allows for setting extensions if available
 * [] : 
 * () : 
 * {} : available settings Dependent on extension

* **TOC** : Table of contents
 * Purpose: Embed a table of content, based on header names.
 * [] : Title of TOC, could default to "Table of contents"
 * () : 
 * {} : 

> This seems forced into the provided syntax. Why is this not a block element? Why is the title provided inside the syntax as opposed to just being text prior to the "TOC" tag? - nexussays 

> Because unless the file can be changed by processor, it's probably safer to just autogenerate the TOC everytime it is rendered. But I don't see any reason it can't be a block directive, just needs a 'generated at date tag' - mofosyne

* **spoiler** : Hides spoilers
 * Purpose: Informs display to hide content, unless user wants to be shown the spoilers
 * [] : Spoiler Text 
 * () : 
 * {} : 

> This usage is completely different than every other tag which wraps text (`\`, `*`, `**`, etc) which would make it both unconventional and very difficult for users. - nexussays 
> I say it's pretty obvious when it say's spoiler. And syntactically [] means content. Don't want to pollute the core syntax. -mofosyne

* **fig** : figure
 * Purpose: create a figure instance
 * [] : `<figname>` name of figure
 * () : 
 * {} : type="numeric/letter/figname"
 * Block Directive Content : Content of figure 

> How is this semantically different to a creator than an image and some text? How would it co-exist with existing syntax for images, and code blocks, both of which are mentioned in the spec as uses for the `<figure>` tag. What would this resolve to in non-HTML implementations? (ie - What "is" a figure?) - nexussays 

> It's used in academia to indicate that a group of images, codes, statistics or data to be referenced in a report. It's used often in latex, and it's bloody annoying. -mofosyne

* **ref** : link to figure 
 * Purpose: link to figure <figname> created from 'fig'
 * [] : 
 * () : figname
 * {} : type="override numeric/letter/figname"

> What is this providing beyond duplicating the link syntax? - nexussays 

> Yea I agree we should probably think about using the `[]:` somehow (if I'm correct that it can act as a figure) -mofosyne

* **asciiArt** : renders ASCII art
 * Purpose: Lets parser knows that the content is to be treated as ASCII art. Output is more flexible.
 * [] : 
 * () : 
 * {} : renderAs='vector/bitmap/ASCII', width="width of image", height="height of image"
 * Block: ASCII art
 * note: rendering could be via taking the average density of each character split as a grid of 3*3 pixel per character.
 * note: Do this but in reverse http://mattmik.com/articles/ascii/ascii.html

* **asciiDiagram** : renders technical ASCII diagram
 * Purpose: Lets parser knows that the content is to be treated as ASCII diagram. (Which unlike ASCII art, has well defined lines, and boxes, text, and should be treated like a technical drawing. E.g. no smoothing or blurring).
 * [] : 
 * () : 
 * {} : renderAs='vector/bitmap/ASCII', width="width of image", height="height of image"
 * Block: ASCII diagram
 * note: could use https://github.com/Frimkron/Ascidia to render it in a pretty manner.

* **wiki** : looks up a wiki page
 * Purpose: in a wiki context, it is a directive to jump to a wiki page. In a normal site context, it references the most popular encyclopaedia wiki site (e.g. wikipedia)
 * [] : wiki page name
 * () : optional direct link
 * {} : 

* **dictionary** : looks up a dictionary
 * Purpose: looks up a local dictionary or user's choice
 * [] : word to reference
 * () : optional direct link to alternative dictionary service
 * {} : 

* **thesaurus** : looks up a thesaurus
 * Purpose: looks up a local thesaurus or user's choice
 * [] : word to reference
 * () : optional direct link to alternative thesaurus service
 * {} : 