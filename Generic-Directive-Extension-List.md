Generic Directives is still in active discussion in http://talk.commonmark.org/t/generic-directives-plugins-syntax . But for brainstorming purposes, here is some possible extensions to support, or at least adhere to if not included. 

It might look like `!extensionName[](){}`

-------

Below is a list of extensions and it's purpose. 

* extensionName : 
 * Purpose: 
 * [] : contentField 
 * () : argumentField 
 * {} : keyValueField 

-----------

* default : default extension
 * Purpose: used if no extension name is specified. Reads url, and chooses the appropriate extensions. E.g. .png will be embedded as an image
 * []  contentField: 
 * () argumentField: Reads the url name to determine filetype
 * {} keyValueField: 

* image : embed image
 * Purpose: embeds image in page
 * []  contentField: image alt text
 * () argumentField: image url
 * {} keyValueField: width="width of image", height="height of image"

* TOC : Table of content
 * Purpose: Embed a table of content, based on header names.
 * []  contentField: 
 * () argumentField: 
 * {} keyValueField: 

* spoiler : Hides spoilers
 * Purpose: Informs display to hide content, unless user wants to be shown the spoilers
 * []  contentField: Spoiler Text 
 * () argumentField: 
 * {} keyValueField: 