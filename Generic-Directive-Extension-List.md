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

* **TOC** : Table of content
 * Purpose: Embed a table of content, based on header names.
 * [] : 
 * () : 
 * {} : 

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

* **fig.`<figname>`** : link to figure <figurename> 
 * Purpose: link to figure <figurename> created from 'fig'
 * [] : 
 * () : 
 * {} : type="override numeric/letter/figname"