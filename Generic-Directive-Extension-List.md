Generic Directives is still in active discussion in http://talk.commonmark.org/t/generic-directives-plugins-syntax . But for brainstorming purposes, here is some possible extensions to support, or at least adhere to if not included. 

It might look like `!extensionName[](){}`

-------

Below is a list of extensions and it's purpose. 

* extensionName : 
 * Purpose: 
 * [] : contentField (Mandatory/Optional)
 * () : argumentField (Mandatory/Optional)
 * {} : keyValueField (Mandatory/Optional)

-----------


* TOC : Table of content
 * Purpose: Embed a table of content, based on header names.
 * []  contentField: (Optional)
 * () argumentField: (Optional)
 * {} keyValueField: (Optional)

* spoiler : Hides spoilers
 * Purpose: Informs display to hide content, unless user wants to be shown the spoilers
 * []  contentField: Spoiler Text (Optional)
 * () argumentField: (Optional)
 * {} keyValueField: (Optional)