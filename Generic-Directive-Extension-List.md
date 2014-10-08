Generic Directives is still in active discussion in http://talk.commonmark.org/t/generic-directives-plugins-syntax . But for brainstorming purposes, here is some possible extensions to support, or at least adhere to if not included. 

It might look like `!extensionName[](){}`

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

* **TOC** : Table of contents
 * Purpose: Embed a table of content, based on header names.
 * [] : Title of TOC, could default to "Table of contents"
 * () : 
 * {} : 

> This seems forced into the provided syntax. Why is this not a block element? Why is the title provided inside the syntax as opposed to just being text prior to the "TOC" tag?

* **spoiler** : Hides spoilers
 * Purpose: Informs display to hide content, unless user wants to be shown the spoilers
 * [] : Spoiler Text 
 * () : 
 * {} : 

* **fig** : figure
 * Purpose: create a figure instance
 * [] : `<figname>` name of figure
 * () : 
 * {} : type="numeric/letter/figname"
 * Block Directive Content : Content of figure 

> How is this semantically different to a creator than an image and some text? How would it co-exist with existing syntax for images, and code blocks, both of which are mentioned in the spec as uses for the `<figure>` tag. What would this resolve to in non-HTML implementations? (ie - What "is" a figure?)

* **ref** : link to figure 
 * Purpose: link to figure <figname> created from 'fig'
 * [] : 
 * () : figname
 * {} : type="override numeric/letter/figname"

> What is this providing beyond duplicating the link syntax?