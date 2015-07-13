This is a list of syntax extensions to standard Markdown/Commonmark found in the documentation of these [[Markdown Flavors]].

## Inline Markup Extensions

`_italic_ __bold__ ___bold italic___ ____underlined____` 
Some implementations go the Textile? way of differentiating semantic (strong) emphasis from presentational italic and boldface markup. Over there, the latter is achieved by doubling asterisk `*` or underscore `_`, markdown flavors instead choose the underscore, single and double, for the purely stylistic meaning and they add another layer with four underscores rendering the enclosed text with an underline, which was the reason for using the underscore in the first place. Fallback for the latter is surprisingly unsatisfactory, though, because some implementations will parse four underscores neither as double bold nor as open and immediate close bold, but something more strange.
* [Test underline syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=*+_italic_%0A*+__bold__%0A*+___bold+italic___%0A*+____underlined__₎
* **Recommendation:** Allow *optional* different treatment of asterisk `*` (semantic) and underscore `_` (presentational) when used as phrase affixes. Only then extend the presentational markup to underlines, using 4 underscores on each side. Also, define the meaning and parsing of more than 3 asterisks or underscores everywhere.

`^superscript^`  
`^^superscript^^`  
`^(superscript)  ^s` 
Superscript text, i.e. positioned above the baseline and usually smaller, can be meaningful, although in many cases, such as chemical molecule formula notation, normal size and position is unambiguous, too. The circumflex or caret character `^` is used for that in TeX and elsewhere already, so it has been adopted in markdown flavors as well, but implementations differ as to whether they require one or two carets as affixes and some even try to make do with just a prefix – at least for single superscript characters, longer runs are then put in parenthesis to avoid ambiguity, e.g. with footnotes.
* [Test superscript syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=*+text%5Eindex%5E%0A*+text%5E%5Eindex%5E%5E%0A*+text%5E(index)%0A*+text%5Ei)
* **Recommendation:** Standardize single circumflex on both sides as part of extended core.

`~subscript~`  
`~~subscript~~`  
`~(subscript)  ~s`  
`_(subscript)  _s` 
Much like superscript, subscript indices etc. may be semantic. TeX and some other languages use the underscore as a prefix (and maybe suffix), so that would be a good choice for markdown, too, had it not been used for emphasis instead. Some implementations try to use it nevertheless, with parentheses as mentioned above. More common, however, is the use of the tilde character `~` akin to the underscore. Note that the (double) tilde is used for deleted or stricken text elsewhere.
* [Test subscript syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=*+text~index~%0A*+text~~index~~%0A*+text~(index)%0A*+text~i%0A*+text_(index)%0A*+text_i)
* **Recommendation:** Standardize single tilde on both sides as part of extended core.

`{-- removed content --}`  
`{~~removed content~>ins~~}`  
`{++ added content ++}`  
`{== highlighted ==}` 
[Critic Markup][CM] is an orthogonal spec to markdown that can be used to annotate text with editorial comments and track changes. It consistently uses curly braces and double-character affixes which may also markup whitespace.  
`~~removed content~~` 
`--removed content--`  
`++added content++`  
`==highlighted==` 
`???highlighted???` 
Several implementations, sometimes by way of plugins, adapt syntax extensions from this, leaving out the braces. The plus `++` for additions and equals `==` for highlighted parts are unproblematic, but double ´hyphen-minus `--` is frequently used to stand in for an en (or sometimes em) dash ‘–’/‘—’, which is why the tilde `~~` is employed instead, although it itself may also clash – with subscript notation. Shorthand replacement markup with `~>` infix is not inherited from CriticMarkup.
One implementation that does not mark up additions and removals has a different affix for highlights, three question marks `???` which may be unambiguous but also unintuitive.
* [Test editorial syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%7B--+removed+content+--%7D+with+%7B%2B%2B+added+content+%2B%2B%7D+or+%7B~~+original+~%3E+changed+~~%7D+and+%7B%3D%3D+highlighted+%3D%3D%7D+CriticMarkup.%0A%0A%7B--removed+content--%7D+with+%7B%2B%2Badded+content%2B%2B%7D+or+%7B~~original~%3Echanged~~%7D+and+%7B%3D%3Dhighlighted%3D%3D%7D+CriticMarkup+without+spaces.%0A%0A~~removed+content~~+or+--removed+content--+with+%2B%2Badded+content%2B%2B+and+%3D%3Dhighlighted%3D%3D+or+%3F%3F%3Fhighlighted%3F%3F%3F+markdown.)
* **Recommendation:** Standardize an optional extension for collaboration, using double affixes (tilde `~~`, plus `++` and equals `==`) without curly braces.

`"short quote"`  
`""cited title""` 
`"""cited title"""` 
Inline quotations and cites of titles, names or terms are rarely considered for extensions, but if so they are marked up with quotation marks. Usually, double-quote affixes ar replaced by “curly” quotation marks by (integrated) typographic preprocessors, but it’s just as intuitive to use HTML `<q>` instead. Cited instances are surrounded by either doubled or tripled marks.
* [Test quote syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=a+%22short+quote%22+with+%22%22cited+title%22%22+or+%22%22%22cited+title%22%22%22)
* **Recommendation:** Standardize an option extension with double double quotes `""` for quotations and triple double quotes `"""` for citations. Single double quotes `"` may be replaced by language-dependent curly quotation marks, e.g. `“` and `”`. Alternatively double and triple angular brackets `<` and `>` could be used, mimicking guillemots.

`>>stripped comment<<` 
`<!--- stripped comment --->` 
`{::COMMENT}stripped comment{:/COMMENT}` 
Some authors want to add comments to source documents that shall not appear at all in the output – or vice versa. No conventional syntax has been established for this. The best backwards compatibility is provided by special HTML comments. Some implementations may employ a generic markup addition, which are discouraged.
* [Test comment syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=*+%3C!--+HTML+comment+--%3E%0A*+%3C!---+special+HTML+comment+---%3E%0A*+%3E%3Eangular+bracket+comment%3C%3C%0A*+%7B%3A%3ACOMMENT%7Dverbose+comment%7B%3A%2FCOMMENT%7D)
* **Recommendation:** Make it standard core behavior to pass through unaltered basic HTML comments with 2 dashes `--` on both sides, but completely remove all HTML comments with 3 or more consecutive dashes `---` on both sides. Visible, editorial comments should be part of the collaboration extension described above, using inverted double angular brackets `>>` and `<<`.

  [CM]: http://criticmarkup.com
  
## Link and Reference Markup Extensions

`http://example.com`
Automatic URL detection and hyperlink generation is implemented often, but implementations differ in the details, i.e. which valid or invalid addresses are recognized and which are not. Usually, at least the colon and the double slashes are required, except for email addresses. Some implementations only auto-convert for known (and safe) protocol schemes.
* [Test direct link syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=*+mail%40example.com%0A*+http%3A%2F%2Fexample.com%0A*+www.example.com%0A*+foo%3A%2F%2Fbar.baz)
* **Recommendation:** Don’t require implementations to parse text for plain URLs, but don’t disallow it either. Reference the Web Addresses specification.

`[myid]: http://example.com (Example site)` 
The optional title in reference-style links follows the address, but it needs to be enclosed somehow. Standard implementations support surrounding single or double quotation marks `'`/`"`, some flavor extend this with round parenthesis. This may be relevant for future extensions that would add even more metadata to links or embedded media.
* [Test parenthetic link title syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%5Breference+link%5D%5Bmyid%5D%2C+%5Binline+link%5D(http%3A%2F%2Fexample.com+(Example))%0A%0A++%5Bmyid%5D%3A+http%3A%2F%2Fexample.com+(Example))
* **Recommendation:** Require implementations to finish reading an URL when they encounter a whitespace character. They must throw away everything that follows if they don’t know what to do with it. The first quoted or parenthesized string becomes the link title, more strings may follow with other extensions.

`[mnemonic target][]`  
`[mnemonic target]`  
`[[mnemonic target]]`  
`[[mnemonic target|text]]` 
Shortcut or implicit links – where the address or identifier can be derived from the title in a straightforward manner – are quite common, too, but the exact syntax differs a bit. Leaving the second pair of square brackets empty is the most common approach (while the reverse is seen nowhere). Leaving them out altogether is even more author-friendly, but it is also prone to become ambiguous or being unintended (hence leading nowhere). Doubling opening and closing brackets is an alternative that has been inherited from wiki syntax, MediaWiki in particular, but its different syntax for link text, which employs a pipe character as separator, is probably not worth consideration, because that can already be done with existing markdown syntax.
* [Test shortcut/implicit link syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%5Bempty+ID%5D%5B%5D%2C+%5Bshortcut%5D%2C+%5B%5Bwiki-style%5D%5D%2C+%5B%5Bwiki-style%7Ctext%5D%5D%0A%0A%5Bempty+ID+ref%5D%5B%5D%2C+%5Bshortcut+ref%5D%2C+%5B%5Bwiki-style+ref%5D%5D%2C+%5B%5Bwiki-style+ref%7Ctext%5D%5D%0A%0A%23+Empty+ID%0A%0A%23+Shortcut%0A%0A%23+Wiki-Style%0A%0A++%5Bempty+ID+ref%5D%3A+http%3A%2F%2Fexample.com%2Femtpyid%0A++%5Bshortcut+ref%5D%3A+http%3A%2F%2Fexample.com%2Fshortcut%0A++%5Bwiki-style+ref%5D%3A+http%3A%2F%2Fexample.com%2Fwiki%0A)
* **Recommendation:** Require support for the empty trailing square bracket notation in the core. As part of a highly recommended smart links module, standardize single bracket syntax `[` and `]` for shortcut links and make sure the inner pair of double bracket enclosures is used, too. Do not support the pipe syntax, i.e. the pipe would be considered part of the reference.

`[^id]` ↩︎ …  
`[^id]: note` 
`^[note]` 
Named and anonymous footnotes or endnotes are implemented the same way everywhere (if at all) and build upon shortcut link markup. The characteristic mark is the circumflex `^` which either precedes the reference identifier or the anonymous inline note inside square brackets.
* [Test footnote syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=named%5B%5Eid%5D+anonymous%5E%5Bnote%5D%0A%0A++%5B%5Eid%5D%3A+footnote%0A)
* **Recommendation:** Standardize a notes module with named and anonymous notes as shown above. Suggest to implementations that they let authors differentiate notes using numeric identifiers from those using textual or mixed ones, e.g. for footnotes vs. endnotes.

`[#id]` ↩︎ …  
`  [#id]: citation`  
`[@id]`  
`[pages etc.][@id]`  
`@id [pages etc.]`
For scientific citations, there are two approaches found in markdown flavors. The first works just like reference footnotes, except that it uses a hash character `#` as identifer prefix. The citation is found verbatim in the document instead of the web address (URL). The second approach uses the at-sign `@` instead and relies on an external biography database. The latter one also supports location/page info in a very basic way.
* [Test citation syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=source%5B%23hashid%5D+and+source%5Bp.+1%5D%5B%40atid%5D%2C+also+just+author+%40atid+%5Bpage+2%5D%0A%0A++%5B%23hashid%5D%3A+citation%0A++%5B%40atid%5D%3A+another)
* **Recommendation:** As part of the **smart links module** and aligned with the **notes module**, use a unified syntax, possibly employing the at-sign `@`, to link to internal and external references.

`ACRO` … ↩︎  
`  *[ACRO]: expansion` 
For abbreviations and acronyms, possibly general technical terms, too, there is a convention that uses reference definitions, too, but finds inline uses automatically. Another difference is that the marker, an asterisk `*`, goes in front of the square brackets in the reference line, which probably was intended to improve fallback, because the abbreviation “glossary” might be rendered as a bullet list this way.  
`[abbr](abbr:expansion)` 
Another approach reuses anonymous inline link syntax by introducing a pseudo-scheme `abbr` for URLs. That should also be possible with reference links, of course.
* [Test abbreviation syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=ACRO+%5Babbr%5D(abbr%3Aexpansion)%0A%0A++*%5BACRO%5D%3A+expansion)
* **Recommendation:** Handle within the **smart links module** or the module covering definition lists.

`[text](class:myclassname)`  
`[text](id:myidentifier)` One flavor also adds pseudo-schemes for generic classes and identifiers. This should fall back nicely, except where URLs are checked deeper for validity, i.e. parsers that will only accept known protocol schemes. 
* [Test generic classes and identifiers](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%5Btext%5D(class%3Amyclassname)+%5Btext%5D(id%3Amyidentifier))
* **Recommendation:** Leave for later as another option for extendability.

`![alt](example.img =640x480)`  
`![alt](example.img "image title" =640x480)`  
`![alt](example.img =640x480 "image title")`
Optional image size may be supplied in some variants after – or before? documentation seems to mismatch implementation – the title, preceded by an equals sign we find width and height in pixels separated by an `x`. Sadly, this breaks badly in several implementations.
* [Test image size syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=*+!%5BVGA%5D(first.png+%3D640x480)%0A*+!%5BSVGA%5D(second.png+%22800+×+600+pixels%22+%3D800x600)%0A*+!%5BDVGA%5D(third.png+%3D960x640+%22960+×+640+pixels%22)%0A*+!%5BXGA%5D%5Bxga%5D%0A*+!%5BXGA%2B%5D%5Bxgaplus%5D%0A*+!%5BSXGA%5D%5Bsxga%5D%0A%0A++%5Bxga%5D%3A+fourth.png+%3D1024x768%0A++%5Bxgaplus%5D%3A+fifth.png+%221152+×+864+pixels%22+%3D1152x864%0A++%5Bsxga%5D%3A+sixth.png+%3D1280x1024+%221280+×+1024+pixels%22%0A)
* **Recommendation:** Require implementations to finish reading an URL when they encounter a whitespace character. They must throw away everything that follows if they don’t know what to do with it. The first quoted or parenthesized string becomes the image title, more strings may be defined within the **inclusion links module**.

`=== [caption]` ↩︎  
`![](figure.img)` ↩︎  
`===`  
↩︎↩︎ `![caption](figure.img)` ↩︎↩︎
Figures, i.e. floating image blocks, with caption can either be derived from standard paragraphs, that contain nothing but a picture link, or with a special fenced block that also contains the normal link. The caption can either be taken from existing `alt` and `title` or it is found as an attribute to the opening fence. Equals signs as fences are problematic, though, ecause they certainly will be taken as heading underlines somewhere.
* [Test figure syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%3D%3D%3D+%5Bcaption%5D%0A!%5B%5D(figure.png)%0A%3D%3D%3D%0A%0A%3D%3D%3D%0A!%5Bno+caption%5D(figure.png)%0A%3D%3D%3D%0A%0A!%5Bcaption%5D(figure.png+%22title%22)%0A%0A)
* **Recommendation:** Strongly suggest that implementations should consider a paragraph containing nothing but images as a floating figure with caption.

`@[youtube](crypticid)` 
There have been various proposals on how to embed videos and other media from external services easily, but only one was found documented in an actual implementation. It just uses an at-sign `@` in place of the exclamation mark of image links. Since it does not accept full URLs as parameters, the fallback to a normal link is not helpful at all.
* [Test embeded foreign media syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%40%5Byoutube%5D(oHg5SJYRHA0))
* **Recommendation:** As part of an **inclusion links module**, select a prefix to normal links to mean embedding. This does not have to end up to be `@`.

`{toc}`  
`[toc]`  
`[[toc]]`  
`@[toc](heading)` 
Many implementations assign unique identifiers to all headings and maybe to other output elements as well. It‘s a simple step from there to supply an automatically generated table of contents, although viewers for output formats like PDF have built-in support for document structure. There are several variants to markup the English keyword `toc` to place this TOC at a certain position inside the document. One flavor uses the same link-based syntax with at-sign `@` as for media embeds. The other variants often align with similar processing instructions as well.  
`{frontmatter}` 
    `{half-title}` 
    `{series-title}` 
    `{title-page}` 
    `{copyright}` 
    `{dedication}` 
    `{epigraph}` 
    `{figures}` 
    `{tables}` 
    `{foreword}` 
    `{preface}` 
    `{acknowledgments}`
    `{introduction}`
    `{abbr}`
    `{chronology}`  
`{mainmatter}` 
    `{pagebreak}`  
`{backmatter}`
    `{appendices}` 
    `{notes}` 
    `{glossary}` 
    `{bibliography}` 
    `{contributors}`  
    `{illustration-credits}` 
    `{index}` 
Two related flavors intended for book publishing include a number of English named processing instructions besides one for the TOC.
* [Test processing instruction syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%7Btoc%7D%0A%0A%5Btoc%5D%0A%0A%5B%5Btoc%5D%5D%0A%0A%40%5Btoc%5D(heading)%0A%0A%23+Level+1%0A%0A%23%23+Level+2%0A)
* **Recommendation:** Do not adopt, but make a note that parsers should provide the user with an option to throw away paragraphs/lines that start and end with matching curly braces. Also allow profiles to overload the semantic meaning of horizontal rules `---`, `___` and `***`. If an output format supports document outlines based upon headings (which are basically TOCs), implementations should aid their generation.

`<<[transclude](file.ext)`  
`<<(file.ext)`  
`{{file.ext}}` Transclusion of external files is helpful for larger projects and with source code. Few flavors support it, though, and syntax differs. One uses embedded link syntax with double less-than `<` instead of the exclamation mark, another employs MediaWiki template syntax with double curly braces.
* [Test transclusion syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%3C%3C%5Btransclude%5D(%2Fetc%2Fpasswd)%0A%0A%3C%3C(%2Fetc%2Fpasswd)%0A%0A%7B%7B%2Fetc%2Fpasswd%7D%7D%0A)
* **Recommendation:** As part of an **inclusion links module**, select a prefix to normal links to mean transclusion. This does not have to end up to be `<<`.

`[-[ QR code ]-]` 
A single implementation offers the exotic possibility to generate quick-response codes inline.
* [Test QR code syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%5B-%5B+http%3A%2F%2Fexample.com%2Fqr+%5D-%5D)
* **Recommendation:** Do not support something like this at this point in time.

## Prefix-only and Symbol Extensions

`@username`  
`#tag`  
`!request`  
`$snippet`  
`~label` 
Twitter-like hash-tags and username mentions are encountered frequently in comment use cases. Sometimes they are not part of the flavor itself, though, but are added by a custom pre or post-processor which knows about the local address structure – for mentions with at-sign, this is basically the same as the respective citation syntax, just with works instead of users. Sometimes user names include group names or special keywords like `@all` and tags are used with a specific meaning, e.g. `@issue` or `@bug`. Note that dollar sign is also used for inline math markup and tilde is also used for subscripts and strike-outs.
* [Test mentions and tag syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=a+%40username+or+%40citekey+with+a+%23tag+or+%23issue+or+%23bug+and+also+a+!request+and+%24snippet+and+~label)
* **Recommendation:** Standardize, as part of an optional **smart links module**, the at `@` and hash `#` affixes with suffixes being optional. Make the target either explicit with a reference line or implicit, hence site-specific and user-defined. Suggest to implementations that authors may want different behavior for numeric identifiers (tag vs. bug).

`:emoji:`  
`:-) ;) )-: <3 (!)` … 
Western-style image or text emoticons (and symbols) use mini character art, where some cases could be ambiguous which makes a curated collection required. 
Japanese-style Unicode emoji are almost always referenced by name inside colon affixes instead. 
* [Test emoticon, emoji and ASCII art](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%3Asmiley%3A+%3Asmile%3A+%3Afrowning%3A%0A%3Aheart%3A+%3A%2B1%3A+%3Aexclamation%3A%0A%0A%3A-%29+%3A%29+%29-%3A+%0A%3C3+!3+%28!%29%0A.oO%28thought%29)
`&auml; &#228; &#xE4;` 
Some implementations – flavors are usually quiet on this – normalize all named and numeric entity references. 
* [Test entity normalization](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%26auml%3B+%26%23228%3B+%26%23xE4%3B)
`\"a \to` 
TeX-style character macros are usually only supported inside a respective math mode.
* [Test character macro syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%5C%22a+%5Crightarrow%0A%5C%5C%22a+%5C%5Crightarrow)
* **Recommendation:** The core spec should require implementations to normalize SGML-like entity references to UTF-encoded characters, with some exceptions as required by the target markup language. This includes all named character entities from HTML5 and all numeric (decimal or hexadecimal) references. 
    The named emoji syntax with English-only designators is not well suited in an international context and therefore cannot be required behavior, even within a module. An optional **art module** should list emoticons that do not clash with Commonmark syntax and have conventional meaning.

## List Extensions

`term` ↩︎ 
`:   definition`  
`term` ↩︎ 
`  ~ definition`  
`=term=` ↩︎ 
`    definition` 
Glossaries and other applications of definition lists seem popular, but there are at least three syntactic variants for them. The definition follows the term in a separate line, often indented or separated by an optional or mandatory blank line or both. While the term lines are left without a prefix in two variants, a colon `:` – most popular – or tilde `~` precedes the definition lines. In another variant, the term is marked with equals `=` affixes instead.
* [Test definition list syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=colon+term%0A%3A+++definition%0A%0A----%0A%0Atilde+term%0A++~+definition%0A%0A----%0A%0A%3Dequals+term%3D%0A++++definition)
* **Recommendation:** There absolutely should be support, in either a **lists module** or a **scientific writing module** or the **table module**, for lists with keys instead of or in addition to bullets, but there is no recommendation yet for a definite syntax.

`2. item with start value`   
`4. item with fix value`  
`A) upper alpha`  
`a) lower alpha`  
`I) upper roman`  
`i) lower roman`  
`#) automatic number` 
In enumerated lists, various flavors honor the first numerator value as a start value for output (auto-numbers continue afterwards), others accept author-defined values for all entries. Some flavors recognize alternate “number” formats, like alphabetic or roman numerals, and may try to keep them in the output. Usually, digit one ‘1’ followed by either dot `.` or close parentheses `)` can be used for each and every enumerated list item to get automatic numbering, the number sign `#` can be used for the same effect in some flavors, which should be more intuitive, but this will be misinterpreted as a top-level heading in some other implementations.
* [Test explicit numbered list syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=2.+two%0A4.+three%0A%0A____%0A%0A2%29+two%0A4%29+four)
* [Test alternate numbered lists syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=A.+upper+alpha%0A%0A____%0A%0Aa%29+lower+alpha%0A%0A____%0A%0AI.+upper+roman+or+9th+alpha%0A%0A____%0A%0Ai%29+lower+roman%0Aii%29+to+dismabiguate)
* [Test automatically numbered list syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%23%29+automatic+number%0A%0A____%0A%0A%23.+again%0A)
* **Recommendation:** Only standardize support for decimal, alphabetic and automatic numbering, but not roman numerals. Alphabetic counters may be divided into upper and lower case. The spec should reference CSS Counter Styles for details (e.g. aa, ab, ac vs. aa, bb, cc). Auto-enumeration should also be part of the core, but – depending on backwards compatibility – may be achieved by leaving out the digit or letter completely instead of replacing it by the number sign `#`.

`+ bullet list item`  
`- [ ] to do: open task list item`  
`- [X] done: closed task list item` 
Besides dash `-` and asterisk `*`, the plus sign can be used in many flavors for bullet-point lists. Some flavors tailored to development and collaboration feature (non-interactive) task lists, where the bullet character is followed by a pair of square brackets that is either empty, i.e. just has (optional) whitespace inside, or is checked with an `X` or certain other characters (e.g. plus sign `+` or asterisk `*`).
* [Test bullet list syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=*+asterisk+%2F+star%0A-+hyphen-minus+%2F+dash%0A%2B+plus)
* [Test nested list syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=*+first+level%0A**+second+level%0A*+first+level%0A++*+second+level%0A*+first+level%0A++%2B+second+level)
* [Test task list syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=-+%5B+%5D+to+do%0A-+%5BX%5D+done%0A)
* **Recommendation:** Require support for `+`, `-` and `*` list bullets in the core specification. Handle checkboxes etc. in an optional **(pseudo) forms module**. Specific profiles may assign narrower semantics, such as “task list”, to certain syntax patterns, but this should not be part of the core or the syntax extension modules. The same goes for “pro-con lists”, “release notes”, “diff” etc.

## Paragraph and Block Extensions

`>! spoiler`  
`-> center <-` 
`C> center`  
`A> aside` 
`D> discussion` 
`E> error` 
`I> information` 
`Q> question` 
`T> tip` 
`W> warning` 
`X> exercise`  
`B> blurp` 
`G> generic` 
Some flavors add predefined paragraph types and they overload blockquote syntax in one way or the other to do so. An additional mark (or letter) after the greater-than sign will probably have better backwards compatibility than one before it. The selection of paragraph types will always leave some people wanting, so maybe (only) a generic mechanism to add custom classes would be better. Spoiler paragraphs reveal their textual content on hover.
* [Test paragraph type syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%3E!+spoiler%0A%0A-%3E+center+%3C-%0A%0AC%3E+center%0A)
* **Recommendation:** This may be handled by the **info string module**, but no final recommendation is given here.

`> (http://example.com/source) quote` 
One flavor adds the possibility to add a URL reference to block quotations. It is put in parentheses directly after the first line prefix `>`.
* [Test sourced blockquote syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%3E+%28http%3A%2F%2Fexample.com%2Fsource%29+quote)
* **Recommendation:** No final recommendation is provided. It would be at least as useful to parse the line or paragraph above the block quote if it ends with a colon `:`. Another common pattern to specify sources is a line introduced by 2 dashes `--` that is placed immediately after the block quote.

`> %class%` ↩︎ 
`> prefixed block`  
`::: class` ↩︎
`fenced block` ↩︎ 
`:::`  
`!!! class` ↩︎ 
`    indented block` 
Generic blocks of text with author-defined classes allow much freedom. There is no consensus among flavors how to deal with them, though. One implementation uses special-cased block quotation markup, another has proprietary colon `:` fences (without good fallback behavior) and the third one introduces indented lines with a special, `!` fence-like header (falling back to code).
* [Test generic block syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%7B.class%7D%0AG%3E+attributed+block%0A%0A%3E+%25class%25%0A%3E+prefixed+block%0A%0A%3A%3A%3A+class%0Afenced+block%0A%3A%3A%3A%0A%0A!!!+class%0A++++indented+block%0A)
* **Recommendation:** Reuse existing backtick or tilde fences for this, employing the **info string module**.

## Scientific and Other Extensions

`(@) anonymous numbered example`  
`(@id) named numbered example` 
Some texts, e.g. linguistic articles, use paragraph-like examples that are numbered consecutively throughout the whole document; they are reference by number within the surrounding text frequently. One flavor adds list-like syntax for this, with an at-sign (inside parentheses) which may be followed by an identifier. References are made with this, too, which aligns nicely with the respective citation syntax.
* [Test numbered examples syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%28%40xmp%29+named+example%0A%0AIntermission%0A%0A%28%40%29+anonymous+example+referencing+%40xmp%0A)
* **Recommendation:** As part of the **smart links module**, adopt a method to assign automatic and arbitrary identifiers to blocks so they can be referenced, and also specify a syntactically related way to reference these of course – this may employ the at-sign `@`. As part of a **list module**, make the counter of certain enumerated lists continuous throughout the document, a pair of parentheses `()` instead of just a closing one `)` seems like a reasonable indicator for that.

`| line-based text` 
Some kinds and pieces of text have meaningful linebreaks and may also use semantic indentation, e.g. poems and postal addresses. One implementation uses the pipe `|` line prefix for these, although that may be interpreted as single-column table in other flavors.
* [Test pre-wrap block syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%7C+a+poem++or++an+address%0A%7C+that+is+what+this+test%0A%7C++++++++++++++will+test%0A)
* **Recommendation:** As part of a **table module**, special-case single-column tables to support this, but make support for it optional.

`~~~math` ↩︎ … `~~~`  
`~~~poem` ↩︎ … `~~~`  
`~~~art` ↩︎ … `~~~` 
Fenced blocks (with three backticks `` ` `` or tildes `~`) were introduced to markup code listings and they can be tagged with the name of the programming language used to faciliate colorful highlighting for enhanced readability. Some flavors extend this to other types as well which may be interpreted to render differently, e.g. mathematical formulas, poems (see also above) or character art and diagrams. Look directly above and below for alternate, specialized syntax.
* [Test fenced content syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%60%60%60math%0Ax%5E2+%5Cto+%5Cfrac12%0A%60%60%60%0A%0A%60%60%60poem%0AOh%2C+brother%2C+where+art%0A+++++++++++++++++++art%3F%0A%60%60%60%0A%0A%60%60%60art%0A%2F%5E%5C%0A%7C_%7C+home+sweet+home%0A%60%60%60%0A)
* **Recommendation:** Make only tilde fences optionally evaluated, i.e. backtick fences are always displayed verbatim (except for color, font and other style changes). Create an optional **info string module** that lists recognized code languages and other identifiers with expected rendering.

`$math$` 
`\(math\)` 
`\\(math\\)` 
`{$$}math{/$$}`  
`$$math$$`  
`\[math\]`  
`\\[math\\]` 
Many flavor allow math to be embedded. Since these formulas often use TeX-like code (less often ASCIImath or MathML), it is reasonable to use TeX-inspired affixes, most with leading backslash, to mark it up. Both inline and block math (equations) is usually possible.
* [Test math syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=Inline+%24m*c%5E2%24+or+%5C(m+%5Ccdot+g%C2%A0%5Ctimes+h%5C)+or+%5C%5C(%3D+E%5C%5C)+or+%7B%24%24%7D%3D+W%7B%2F%24%24%7D%0A%0A%24%24E+%3D+m*c%5E2%24%24%0A%0A%5C%5BE+%3D+m*c%5E2%5C%5D%0A%0A%5C%5C%5BE+%3D+m*c%5E2%5C%5C%5D)
* **Recommendation:** Use fenced syntax above for math blocks, e.g. a full proof. Standardize single dollar affixes for inline math in a dedicated **math module**. As a part of this, invent numbered equation/formula syntax, e.g. `($)` line prefix.

## Metadata Extensions

`% Markdown Extensions` ↩︎ 
`% Christoph Päper` ↩︎ 
`% 2015-07-03`  
`---` ↩︎
`Title: Markdown Extensions` ↩︎
`---` or `...` 
When markdown is used to produce a complete document instead of just fragments of one, it proves useful to be able to assign some metadata to it that is not necessarily shown directly to the reader, although that would not harm either. 
One custom approach has three percent-prefixed lines for title, author and date, which is enough to generate the most basic title pages. Another allows embedding YAML metadata in key-value pairs, where values may be of various types. The latter employs dashed lines as fences, which nicely render as horizontal rules in non-supporting implementations.  
`[%Title]` 
One flavor even makes these metadata values accessible inside the text as template variables.
* [Test document metadata syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%25+My+Title%0A%25+My+Alias%0A%25+2015-07-03%0A%0AText)
* [Test dotted YAML syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=---%0ATitle%3A+My+Title%0AAuthor%3A+My+Alias%0ADate%3A+2015-07-03%0A...%0A%0AText)/[dashed](http://johnmacfarlane.net/babelmark2/?normalize=1&text=---%0ATitle%3A+My+Title%0AAuthor%3A+My+Alias%0ADate%3A+2015-07-03%0A---%0A%0AText) 
    (Please note that Babelmark 2 is tailored to fragments, not documents.)
* **Recommendation:** Adopt YAML with mandatory dashed top and bottom fence `---` (for better backwards compatibility than `...`) in a **metadata module**. Only require support for a single instance at the very top of the document.

`{: #id .class attr="value"}`  
`{#id .class attr="value"}` 
Several flavors satisfy authors’ desire to assign unique identifiers, classes and arbitrary key-value attributes to blocks or even any marked-up span. They all employ curly braces for this, but differ in positions allowed. One implementation tries to be more unambiguous (though less intuitive) by requiring a colon `:` as the first character inside the braces. Identifers are prefixed with a hash mark `#`, class names with a period `.` – just like in CSS selectors. There usually is an equals sign `=`, not a colon, between key and value, the latter may be required to be put in quote marks, at least if cobtaining whitespace or equal signs. The order inside the braces is usually keft to the author’s taste, although id-classes-attributes seems most common and logical.
* [Test generic attribute syntax](http://johnmacfarlane.net/babelmark2/?normalize=1&text=%7B%23id01+.class+title%3D%22a+heading%22%7D%0A%23+Attribute+above%0A%0A%23+Attribute+below%0A%7B%23id02+.class+title%3D%22a+heading%22%7D%0A%0A%23+Attribute+after+%7B%23id03+.class+title%3D%22a+heading%22%7D%0A%0A%23+Attribute+after+suffix+%23+%7B%23id04+.class+title%3D%22a+heading%22%7D%0A%0AAttribute+below+line%0A%3D%3D%3D%3D%0A%7B%23id05+.class+title%3D%22a+heading%22%7D%0A%0AAttribute+after+line%0A%3D%3D%3D%3D+%7B%23id06+.class+title%3D%22a+heading%22%7D%0A%0AAttribute+above+line%0A%7B%23id07+.class+title%3D%22a+heading%22%7D%0A%3D%3D%3D%3D%0A%0A____%0A%0A%7B%3A+%23id08+.class+title%3D%22a+heading%22%7D%0A%23+Colon+attribute+above%0A%0A%23+Colon+attribute+below%0A%7B%3A+%23id09+.class+title%3D%22a+heading%22%7D%0A%0A%23+Colon+attribute+after+%7B%3A+%23id10+.class+title%3D%22a+heading%22%7D%0A%0A%23+Colon+attribute+after+suffix+%23+%7B%3A+%23id11+.class+title%3D%22a+heading%22%7D%0A%0AColon+attribute+below+line%0A%3D%3D%3D%3D%0A%7B%3A+%23id12+.class+title%3D%22a+heading%22%7D%0A%0AColon+attribute+after+line%0A%3D%3D%3D%3D+%7B%3A+%23id13+.class+title%3D%22a+heading%22%7D%0A%0AColon+attribute+above+line%0A%7B%3A+%23id14+.class+title%3D%22a+heading%22%7D%0A%3D%3D%3D%3D%0A)
* **Recommendation:** Don’t adopt, but make a note that parsers should provide the user with an option to throw away paragraphs/lines that start and end with matching curly braces.

## Table Extensions

There are several similar, but partially incompatible approaches to mark up tables. They variously use a combination of vertical pipe `|` and horizontal dash `-` with whitespace alignment to draw rows and columns, hence cells. Other characters like plus `+`, colon `:` and equals `=` are also frequently used. Tables may be split into head, body and foot, both horizontally and vertically, and cells may span several columns or rows or both, but only in a rectangular way, and they may contain multiple lines or proper block content – flavors differ in what they support of all this.

**Details to be added soon**

* **Recommendation:** 
