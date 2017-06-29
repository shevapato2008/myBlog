---
layout: post
title: An Introduction to Markdown Syntax
meta: This is intended as a quick reference and showcase of Markdown syntax.
---

This is intended as a quick reference and showcase of Markdown syntax.

&nbsp;

### **1. &nbsp; Headers**
- - -

**Code**
```
# H1
## H2
### H3
#### H4
##### H5
###### H6

Alternatively, for H1 and H2, an underline-ish style:

Alt-H1
======

Alt-H2
------
```

**Output**  
# H1
## H2
### H3
#### H4
##### H5
###### H6

Alternatively, for H1 and H2, an underline-ish style:

Alt-H1
======

Alt-H2
------

&nbsp;

### **2. &nbsp; Emphasis**
- - -

**Code**
```
Emphasis (a.k.a. italics): 
*asterisks*, or
_underscores_

Strong emphasis (a.k.a. bold):
**asterisks**, or
__underscores__

Combined emphasis:
**asterisks and _underscores_**.

Strikethrough: uses two tildes.
~~Scratch this.~~
```

**Output**  
Emphasis (a.k.a. italics): 
*asterisks*, or
_underscores_

Strong emphasis (a.k.a. bold):
**asterisks**, or
__underscores__

Combined emphasis:
**asterisks and _underscores_**.

Strikethrough: uses two tildes.
~~Scratch this.~~

&nbsp;

### **3. &nbsp; Lists**
- - -

**_Note: In this example, leading and trailing spaces are shown with dots._**

**Code**
```
1. First ordered list item
2. Another item
  * Unordered sub-list (two leading spaces)
1. Actual number doesn't matter, it's just a number.
  1. Ordered sub-list
4. And another item.

   You can have properly indented paragraphs within list items. Notice the blank line above, and the leading spaces (at least one, but we'll use three here to also align the raw Markdown).

   To have a line break without a paragraph, you will need to use two trailing spaces. (two trailing spaces here)  
   **_Note that this is a separate line, but within the same paragraph._** (two trailing spaces here)  
   (This is contrary to the typical GFM line break behaviour, where trailing spaces are not required.)

Unordered list can use
* asterisks
- Or minuses
+ Or pluses

```

**Output**  
1. First ordered list item
2. Another item
  * Unordered sub-list (two leading spaces)
1. Actual number doesn't matter, it's just a number.
  1. Ordered sub-list
4. And another item.

   You can have properly indented paragraphs within list items. Notice the blank line above, and the leading spaces (at least one, but we'll use three here to also align the raw Markdown).

   To have a line break without a paragraph, you will need to use two trailing spaces. (two trailing spaces here)  
   **_Note that this is a separate line, but within the same paragraph._** (two trailing spaces here)  
   (This is contrary to the typical GFM line break behavior, where trailing spaces are not required.)

Unordered list can use
* asterisks
- Or minuses
+ Or pluses

&nbsp;

### **4. &nbsp; Links**
- - -

There are two ways to create links.

**Code**
```
[I'm an inline-style link](https://www.google.com)

[I'm an inline-style link with title](https://www.google.com "Google's Homepage")

[I'm a reference-style link][Arbitrary case-insensitive reference text]

[I'm a relative reference to a repository file](../blob/master/LICENSE)

[You can use numbers for reference-style link definitions][1]

Or leave it empty and use the [link text itself].

URLs and URLs in angle brackets will automatically get turned into links. 
http://www.example.com or <http://www.example.com> and sometimes 
example.com (but not on Github, for example).

Some text to show that the reference links can follow later.

[arbitrary case-insensitive reference text]: https://www.mozilla.org
[1]: http://slashdot.org
[link text itself]: http://www.reddit.com
```

**Output**  
[I'm an inline-style link](https://www.google.com)

[I'm an inline-style link with title](https://www.google.com "Google's Homepage")

[I'm a reference-style link][Arbitrary case-insensitive reference text]

[I'm a relative reference to a repository file](../blob/master/LICENSE)

[You can use numbers for reference-style link definitions][1]

Or leave it empty and use the [link text itself].

URLs and URLs in angle brackets will automatically get turned into links. 
http://www.example.com or <http://www.example.com> and sometimes 
example.com (but not on Github, for example).

Some text to show that the reference links can follow later.

[arbitrary case-insensitive reference text]: https://www.mozilla.org
[1]: http://slashdot.org
[link text itself]: http://www.reddit.com

&nbsp;

### **5. &nbsp; Images**
- - -

**Code**
```
Here's our logo (hover to see the title text):

Inline-style:
![alt text](https://github.com/shevapato2008/blog/raw/gh-pages/assets/images/posts/2017-06-21/icon1.png "Logo Title Text 1")

Reference-style:
![alt text][logo]

[logo]: https://github.com/shevapato2008/blog/raw/gh-pages/assets/images/posts/2017-06-21/icon1.png "Logo Title Text 2"
```

**Output**  
Here's our logo (hover to see the title text):

Inline-style:
![alt text](https://github.com/shevapato2008/blog/raw/gh-pages/assets/images/posts/2017-06-21/icon1.png "Logo Title Text 1")

Reference-style:
![alt text][logo]

[logo]: https://github.com/shevapato2008/blog/raw/gh-pages/assets/images/posts/2017-06-21/icon1.png "Logo Title Text 2"

&nbsp;

### **6. &nbsp; Code and Syntax Highlighting**
- - -

Code blocks are part of the Markdown spec, but syntax highlighting isn't. However, many renderers -- like Github's and _Markdown Here_ -- support syntax highlighting. Which languages are supported and how those language names should be written will vary from renderer to renderer. _Markdown Here_ supports highlighting for dozens of languages (and not-really-languages, like diffs and HTTP headers).  

To see the complete list, and how to write the language names, see the [highlight.js demo page](https://highlightjs.org/static/demo/).

**(1) Inline Code Highlighting**  

**Code**
```
Inline `code` has `back-ticks around` it.
```

**Output**  
Inline `code` has `back-ticks around` it.

**(2) Code Block Highlighting**  

Blocks of code are either fenced by lines with three back-ticks ```, or are indented with four spaces. I recommend only using the fenced code blocks -- they're easier and only they support syntax highlighting.

**Code**
````
```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```

```python
s = "Python syntax highlighting"
print s
```

```
No language indicated, so no syntax highlighting. 
But let's throw in a <b>tag</b>.
```
````

Instead of using ` ```` `, you can also use `~~~` for highlighting multiple blocks of code. Please refer to the following post.  
[How do I escape three backticks surrounded by a codeblock in markdown?](https://stackoverflow.com/questions/31825237/how-do-i-escape-three-backticks-surrounded-by-a-codeblock-in-markdown "StackOverflow")

**Output**  
```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```
 
```python
s = "Python syntax highlighting"
print s
```
 
```
No language indicated, so no syntax highlighting in Markdown Here (varies on Github). 
But let's throw in a <b>tag</b>.
```
&nbsp;

### **7. &nbsp; Tables**
- - -

Tables aren't part of the core Markdown spec, but they are part of GFM and Markdown Here supports them.
They are an easy way of adding tables to your email -- a task that would otherwise require copy-pasting from another application.

**Code**
````

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

+ Colons `:` can be used to align columns.
+ There must be at least 3 dashes `---` separating each header cell.
+ The outer pipes `|` are optional, and you don't need to make the raw Markdown line up prettily.
+ You can also use inline Markdown.

Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3
````

**Output**

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

+ Colons `:` can be used to align columns.
+ There must be at least 3 dashes `---` separating each header cell.
+ The outer pipes `|` are optional, and you don't need to make the raw Markdown line up prettily.
+ You can also use inline Markdown.

Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3

&nbsp;

### **8. &nbsp; Blockquotes**
- - -

**Code**
```
> Blockquotes are very handy in email to emulate reply text. **_(two trailing spaces)_**  
> This line is part of the same quote.

**_Quote break._**

> This is a very long line that will still be quoted properly when it wraps. Oh boy let's keep writing to make sure this is long enough to actually wrap for everyone. Oh, you can *put* **Markdown** into a blockquote.
```

**Output**  
> Blockquotes are very handy in email to emulate reply text. **_(two trailing spaces)_**  
> This line is part of the same quote.

**_Quote break._**

> This is a very long line that will still be quoted properly when it wraps. Oh boy let's keep writing to make sure this is long enough to actually wrap for everyone. Oh, you can *put* **Markdown** into a blockquote.

&nbsp;

### **9. &nbsp; Inline HTML**
- - -

You can also use raw HTML in your Markdown, and it'll mostly work pretty well.

**Code**
```
<dl>
	<dt>Definition list</dt>
	<dd>Is something people use sometimes.</dd>
	<dt>Markdown in HTML</dt>
	<dd>Does *not* work **very** well. Use HTML <em>tags</em>.</dd>
</dl>
```
**Output**  
<dl>
	<dt>Definition list</dt>
	<dd>Is something people use sometimes.</dd>
	<dt>Markdown in HTML</dt>
	<dd>Does *not* work **very** well. Use HTML <em>tags</em>.</dd>
</dl>

&nbsp;

### **10. &nbsp; Horizontal Rule**
- - -

**Code**
```
Three or more...
+ Hyphens `-`
+ Asterisks `*`
+ Underscores `_`

---
***
___

```

**Output**  
Three or more...
+ Hyphens `-`
+ Asterisks `*`
+ Underscores `_`

---
***
___

&nbsp;

### **11. &nbsp; Line Breaks**
- - -

My basic recommendation for learning how line breaks work is to experiment and discover --
hit <Enter> once (i.e., insert one newline), then hit it twice (i.e., insert two newlines),
see what happens. You'll soon learn to get what you want. "Markdown Toggle" is your friend.

Here are some things to try out:

**Code**
```
Here's a line for us to start with.</br></br>
This line is separated from the one above by two newlines, so it will be a *separate paragraph*.

This line is also a separate paragraph, but...</br>
This line is only separated by a single newline, so it's a separate line in the *same paragraph*.
```

**Output**  
Here's a line for us to start with.</br></br>
This line is separated from the one above by two newlines, so it will be a *separate paragraph*.

This line is also a separate paragraph, but...</br>
This line is only separated by a single newline, so it's a separate line in the *same paragraph*.

(Technical note: Markdown Here uses **_GFM line breaks_**, so **_there's no need to use MD's two-space line breaks_**.)

&nbsp;

### **12. &nbsp; YouTube Videos**
- - -

To be continued...

