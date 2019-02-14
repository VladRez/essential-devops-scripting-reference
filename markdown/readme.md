# Markdown

Markdown is a text format and conversion tool for people who write documents.

+ Plain text format, means you can create markdown using simple plain characters in any editor.
  + designed to be written with even the simplist text editors.
  + Easy to read, Easy to write, designed to 
  + Easy to parse, export to web or pdf.
  + .md extension.
  + Renders to html. 
  + stackedit.io Online markdown editor. 

 ## Basics

 ### span elements


+ `**strong**` double asterisk to bold words **strong**
+ Double return characters render `<p>`
  + Multiple Double returns still renders a single `<p>`
+ \` var i = function()\` - renders with `<code>` tags `var i = function()`
  + \\\` - `\` to escape special characters
+ In-line html `<span class="co-sm-3"></span>`
+ tab - renders `<pre><code> text </pre><code>`
  + 4 spaces do the same. 

+ `<br>` two spaces and a carriage return to render

### headlines

C text
+ `===` under text renders headline 1 `<h1>`
+ `---` under text renders headline 2 `<h2>`

ATX

+ `# Headline` h1
+ `## Headline` h2
+ `### Headline` h3
+ up to six, anything over will be literal hashtag

### Block quotes

+ `>` renders as a block quote
+ `>>` renders as a block quote inside a block quote

### Horizontal rules

+ `---`/`___`/`***` reders `hr`


### Unordered Lists
+ `*` / `+` / `-`
  + Indentation creates sublist
+ `1. `

### Links

Inline:
+ `[title](url)`
+ `<http://>`
+ `<email@email.com>`
+ Example of reference `[link][1]` reference, bottom of the document `[1]: "https://.."`
+ `![image_title](image_url)` 
  + `![image_title](image_url "Title")`
+ `![image_title][1]`
+ `[![image_title](image_url "Title")](url)` linkable url


## Github Flavored Markdown

+ underscores are ignored
+ Strikethrough `~~strike~~`
+ check boxes `[x] task 1`
+ auto hotlink - all http's will be links
+ fenced code box, adding a language to the fence will markup the syntax differently based on language. 

### tables

```md
header | header | header
----|----|----
value | value | value

value | value | value

value | value | value

To retail the position:

header | header | header
----|----|----
|| value

| value |

| value | value

```

+ `:---` right align
+ `:---:` center align
+ `---:` left align


