---
layout: post
title: An Introduction to Markdown Syntax
meta: This is intended as a quick reference and showcase of Markdown syntax.
---


This covers the basics of using markdown cells. You can think of markdown cells as documention for your code with extended features.

- [IPython Documentation](http://ipython.readthedocs.io/en/stable/index.html)
- [nbviewer](http://nbviewer.ipython.org/)

### 1. Headers
---

#### Code

```markdown
# Head 1
## Head 2
### Head 3
#### Head 4

Alt Heading 1
===

Alt Heading 2
---
```

#### Output

# Head 1
## Head 2
### Head 3
#### Head 4

Alt Heading 1
===

Alt Heading 2
---

<br><br>

### 2. Emphasis
---

#### Code

(2.1) _Italics_

```markdown
- *Italic*
- _Italic_
```

(2.2) _Strong_

```markdown
- **Bold**
- __Bold__
```

(2.3) _Strikethrough_

```markdown
- ~~Throught~~
```

#### Output

(2.1) _Italics_
 - *Italic*
 - _Italic_

(2.2) _Strong_
 - **Bold**
 - __Bold__

(2.3) _Strikethrough_
 - ~~Throught~~

<br><br>

### 3. Lists
---

#### Code

(3.1) Unordered Lists

Creating simple lists (unordered lists) is done by using plus (+), hyphens (-) or asterisks (*) as list markers. These list markers are interchangeable.

```markdown
- Item 1
+ Item 2
* Item 3
```

(3.2) Ordered List

Number does not matter.

```markdown
1. Item 1
2. Item 2
  1. Sub Item 1
  2. Sub Item 2
5. Item 3
10. Item 4
5. Item 5
```

(3.3) Nested List

Nest a list requires you to indent by **exactly** four spaces.

```markdown
+ Sub Item 1
    - Subsub Item 1
        * Subsubsub Item 1
        * Subsubsub Item 2
    - Subsub Item 2
    - Subsub Item 3
+ Sub Item 2
+ Sub Item 3
```

(3.4) Mixed List

```markdown
1. Item 1
2. Item 2
 + Sub Item 1
     - Subsub Item 1
         * Subsubsub Item 1
         * Subsubsub Item 2
     - Subsub Item 2
     - Subsub Item 3
 + Sub Item 2
3. Item 3
```

#### Output

(3.1) Unordered Lists

Creating simple lists (unordered lists) is done by using plus (+), hyphens (-) or asterisks (*) as list markers. These list markers are interchangeable.

- Item 1
+ Item 2
* Item 3

(3.2) Ordered List

Number does not matter.

1. Item 1
2. Item 2
  1. Sub Item 1
  2. Sub Item 2
5. Item 3
10. Item 4
5. Item 5

(3.3) Nested List

Nest a list requires you to indent by **exactly** four spaces.

+ Sub Item 1
    - Subsub Item 1
        * Subsubsub Item 1
        * Subsubsub Item 2
    - Subsub Item 2
    - Subsub Item 3
+ Sub Item 2
+ Sub Item 3

(3.4) Mixed List

1. Item 1
2. Item 2
 + Sub Item 1
     - Subsub Item 1
         * Subsubsub Item 1
         * Subsubsub Item 2
     - Subsub Item 2
     - Subsub Item 3
 + Sub Item 2
3. Item 3

<br><br>

### 4. Links
---

#### Code

(4.1) Inline

```markdown
https://www.google.com

[Google](https://www.google.com)

[Google with title (hover)](https://www.google.com "Google's Homepage")
```

(4.2) Reference

```markdown
This is a guide on [Markdown][1].

[1]: http://en.wikipedia.org/wiki/Markdown        "Markdown in Wikipedia"
```

#### Output

(4.1) Inline

https://www.google.com

[Google](https://www.google.com)

[Google with title (hover)](https://www.google.com "Google's Homepage")


(4.2) Reference

This is a guide on [Markdown][1].

[1]: http://en.wikipedia.org/wiki/Markdown        "Markdown in Wikipedia"

<br><br>

### 5. Blockquotes
---

#### Code

```markdown
> This is blockquoted text.
>
> This is a second paragraph within the blockquoted text.
```

#### Output
> This is blockquoted text.
>
> This is a second paragraph within the blockquoted text.

<br><br>

### 6. Line Return / Line Break
---

#### Code

(6.1) Press Enter

```markdown
Forcing a line-break
Next line in the list
```

(6.2) Press Enter twice

```markdown
Forcing a line-break

Next line in the list
```

(6.3) Add HTML br tag

```markdown
Forcing a line-break <br>
Next line in the list
```

#### Output

(6.1) Press Enter

Forcing a line-break
Next line in the list

(6.2) Press Enter twice

Forcing a line-break

Next line in the list

(6.3) Add HTML br tag

Forcing a line-break <br>
Next line in the list

<br><br>

### 7. Horizontal Rules
---

You can create a horizontal rule by placing **3 or more** asterisks (*), hyphens (-), or underscores (_) on a single line. Spaces between them is allowed.

##### Code

(7.1) Asterisks

```markdown
***
(Line break)
* * *
(Line break)
**********
```

(7.2) Hyphens

```markdown
---
(Line break)
- - -
(Line break)
----------
```

(7.3) Underscores

```markdown
___
(Line break)
_ _ _
(Line break)
__________
```

#### Output

(7.1) Asterisks

***

* * *

**********


(7.2) Hyphens

---

- - -

----------


(7.3) Underscores

___

_ _ _

__________

<br><br>


### 8. Images
---

#### Code

```markdown
![Alt Text](http://www.google.com/logos/2012/turing-doodle-static.jpg "Alan Turing's 100th Birthday")
```

#### Output

![Alt Text](http://www.google.com/logos/2012/turing-doodle-static.jpg "Alan Turing's 100th Birthday")

<br><br>

### 9. Code and Syntax Highlighting
---

#### Code

````
```python
s = "Python syntax highlighting"
print s
```

```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```

```
No language indicated, so no syntax highlighting.
But let's throw in a <b>tag</b>.
```
````

#### Output

```python
s = "Python syntax highlighting"
print s
```

```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```

```
No language indicated, so no syntax highlighting.
But let's throw in a <b>tag</b>.
```

<br><br>

### 10. Tables
---

#### Code

```markdown
| Website   | URL           | Rank |
| ---------:|:-------------:| ----:|
| Google    | google.com    | 1    |
| Facebook  | facebook.com  | 2    |
| Youtube   | youtube.com   | 3    |
```


#### Output

| Website   | URL           | Rank |
| ---------:|:-------------:| ----:|
| Google    | google.com    | 1    |
| Facebook  | facebook.com  | 2    |
| Youtube   | youtube.com   | 3    |

<br><br>

### 11. HTML
---

#### Code

```markdown
<hr>
<p>Almost any <strong>HTML</strong> code will render<br />Just <i>fine</i>.</p>
```

#### Output

```html
<hr>
<p>Almost any <strong>HTML</strong> code will render<br />Just <i>fine</i>.</p>
```

### 12. Unicode
---

If you can think of any symbol, it is available in unicode.

#### Code

```markdown
- ©
- ®
- ™
```

#### Output

- ©
- ®
- ™

<br><br>

### 13. YouTube Videos
---

#### Code

They can't be added directly but you can add an image with a link to the video like below.

(13.1) Use HTML a tag

```html
Format:
<a href="http://www.youtube.com/watch?feature=player_embedded&v=YOUTUBE_VIDEO_ID_HERE
" target="_blank"><img src="http://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg"
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>

Example:
<a href="http://www.youtube.com/watch?feature=player_embedded&v=R6Sh58B3cOE
" target="_blank"><img src="http://img.youtube.com/vi/R6Sh58B3cOE/0.jpg"
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>
```

(13.2) Use Markdown but at the cost of image sizing and border:

```markdown
Format:
[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://www.youtube.com/watch?v=YOUTUBE_VIDEO_ID_HERE)

Example:
[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/R6Sh58B3cOE/0.jpg)](https://www.youtube.com/watch?v=R6Sh58B3cOE)
```

**_Note:_** Youtube Video ID:

![ALT TEXT](https://docs.joeworkman.net/assets/rapidweaver/stacks/youtube/youtube-faq.png "Youtube Video ID")

#### Output

(13.1) Use HTML a tag

<a href="http://www.youtube.com/watch?feature=player_embedded&v=R6Sh58B3cOE
" target="_blank"><img src="http://img.youtube.com/vi/R6Sh58B3cOE/0.jpg"
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>

(13.2) Use Markdown

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/R6Sh58B3cOE/0.jpg)](https://www.youtube.com/watch?v=R6Sh58B3cOE)

<br><br>


### Reference
---

Some good references for Markdown Syntax:
* [Markdown Guide - Basics](http://markdown-guide.readthedocs.io/en/latest/basics.html "Markdown Guide - Basics")
* [Adam Pritchard's Summary](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet "Github ")

<br><br>
