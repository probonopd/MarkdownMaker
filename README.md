![wqe](https://avatars1.githubusercontent.com/u/7837709?s=400&amp;v=4)
# MarkdownMaker

MarkdownMaker is a simple application to make markdown documentation. Markdown is
is a simple markup language to write formatted documents, widely used e.g. in GitHub.
MarkdownMaker is not a replacement of Doxygen or other document generators; MarkdownMaker
purpose and approach is different: it generates markdown only annotated comments and
ignores everything else. Therefore where Doxygen is better for generating comprehensive
documentation of source code, MarkdownMaker adds generates only explicit documentation and
is therefore it is suitable for interface (API) and introductionary (README) documentation.
Also, unlike those other generators, MarkdownMaker just generates markdown.

The generated markdown is optinally rendered, but please note that is only referential and may
differ e.g. from Github's interpretation of the document.

#### Command line
mdmaker &lt;-q&gt; &lt;-o OUTFILE&gt; &lt;INFILES&gt;
* -q , Quiet, no UI, suitable for toolchains.
* -o OUTPUT, Write output to given file, if not given, Save as dialog is shown upon exit. If OUTPUT
is *null* nothing is written and no dialog is shown.
* INFILES, One or more files that are scanned for markdown annotations. Multiple files are joined
as a single output in input order. If input is a markdown file (*.md), that is added as-is.
If no files given a file open dialog is shown.

### Annotations
#### Markdown field
Markdown section starts with __/&lowast;&lowast;__ ( C comment with an extra asterisk).Section ends to __&lowast;/__ (C comment ends). If section line starts with a __*__, that is omitted.
The section can include markdown language. There it is possible to use `code`,
*italic* and other [items](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

#### Tokens
+ __&#x40;toc__, generates table of contents. Items are pointing to &#x40;namespace, &#x40;class and &#x40;function tokens in this document.
+ __&#x40;scope__, starts a generic scope. Scopes are used to divide markdown content.
+ __&#x40;scopeend__, ends any scope (i.e. also namespace and class scope)
+ __&#x40;namespace NAME__, generates a namespace header and starts a scope.
+ __&#x40;class NAME__, generates a class header and starts a scope.
+ __&#x40;function NAME__, just name, no return value or parameters, , generates a function header. The actual function name string is generated from the function declaration that is expected to found immediately after this markdown section.
+ __&#x40;templateparam NAME description__, generates a template parameter header.
+ __&#x40;param NAME description__, generates a parameter header.
+ __&#x40;return description__, generates a description header.
+ __&#x40;brief__, adds a general one-liner
+ __&#x40;date__, injects a current date.
+ __&#x40;style__ TOKEN STYLE-DESCRIPTION, let redefine styles. The STYLE-DESCRIPTION is generated markdown syntax, where %1 represents token's content.
+ __&#x40;raw__ RAW-TEXT, Normally the inserted text is HTML escaped, but that can be bypassed using raw token and RAW-TEXT is HTML interpreted as-is
+ __&#x40;eol__, after &#x40;raw can join lines and then &#x40;eol is used to insert an explicit newline and end the &#x40;raw content.
+ __&#x40;ignore__, The line is ignored from output.

#### Examples
Using Style
```
###### *Axq is published under GNU LESSER GENERAL PUBLIC LICENSE, Version 3*  
###### *Copyright Markus Mertama 2018*, generated at Fri Nov 9 2018 
_____  
```
Using Raw
```
  @raw + __&#x40;return decription__, generates a description header.  
  @eol  
```




See [AxqLib documentation](https://github.com/mmertama/AxqLib/blob/master/Axq.md)
Axq is also used implementation of this utility.
###### Generated by MarkupMaker, (c) Markus Mertama 2018 
