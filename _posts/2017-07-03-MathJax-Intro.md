---
layout: post
title: Get Started with MathJax
meta: This post introduces how to include mathematics in your web pages using MathJax.
---

## Overview
---

MathJax allows you to include mathematics in your web pages, either using LaTeX,
MathML, or AsciiMath notation, and the mathematics will be processed using
JavaScript to produce HTML, SVG or MathML equations for viewing in any modern browser.

For simplicity, this post will only cover how MathJax works with LaTeX.

There are two ways to access MathJax:
- Use the copy of MathJax available from a distributed network service such as `cdnjs.com` (Recommended)
- Download and install a copy of MathJax on your own server, or use it locally on your hard disk.

<br><br>

## Method 1: Using a Content Delivery Network (CDN) - Recommended!
---

The **easiest** way to use MathJax is to link directly to a public installation
available through a Content Distribution Network (CDN). When you use a CDN,
there is **no need to install MathJax** yourself, and you can begin using
MathJax right away.

The CDN will automatically arrange for your readers to download MathJax files
from a fast, nearby server.

### Step 1: Link to MathJax in the web pages that are to include mathematics

Put the following script into the `<head>` block of your document.
```HTML
<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
```

_Note: The version of MathJax may change over time. Check to ensure using the
 latest version._

### Step 2: Put mathematics into your web pages so that MathJax can display it

To put mathematics in your web page, you can use TeX and LaTeX notation, MathML
notation, AsciiMath notation, or a combination of all three within the same
page; the MathJax configuration tells MathJax which you want to use, and how you
plan to indicate the mathematics when you are using TeX/LaTeX or AsciiMath
notation. We will only consider the *LaTeX* case. For more details about the
other two, please refer to this
[documentation](http://docs.mathjax.org/en/latest/start.html "Putting mathematics in a web page").

**TeX and LaTeX input**

Two types of equations:
- **In-Line Mathematics**: ones that occur within a paragraph
- **Displayed Mathematics**: larger equations that appear separated from the
rest of the text on lines by themselves

Their corresponding _default math delimiters_:
- **In-Line Mathematics**: `\(...\)`
- **Displayed Mathematics**: `$$...$$`, `\[...\]`

_Note: `$...$` in-line delimiters are **NOT** used by default. Because `$`
appear too often in non-mathematical settings, which could cause unexpected cases._

If you want to use `$...$` for in-line math mode, you must enable that
explicitly in your configuration:

```HTML
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>
<script type="text/javascript" async src="path-to-mathjax/MathJax.js?config=TeX-AMS_CHTML"></script>
```

<br><br>

## Method 2: Installing Your Own Copy of MathJax
---

### Step 1: Downloading and Installing MathJax

The MathJax source code is hosted on
[GitHub](https://github.com/mathjax/MathJax/ "MathJax").
To install MathJax on your own server, download the latest distribution and
unpack the archive and place the resulting MathJax folder onto your web server
at a convenient location where you can include it into your web pages.

### Step 2: Configuring your copy of MathJax

When you include MathJax into your web pages as described below, it will load
the file `config/TeX-MML-AM_CHTML.js` (i.e., the file named
`TeX-MML-AM_CHTML.js` in the `config` folder of the main `MathJax` folder).

### Step 3: Linking your copy of MathJax into a web page

You can include MathJax in your web page by putting the following code in your document’s `<head>` block.

```HTML
<script type="text/javascript" async src="path-to-MathJax/MathJax.js?config=TeX-MML-AM_CHTML"></script>
```

It is also possible to load MathJax into the `<body>` section, if needed.
If you do this, load it as early as possible, as MathJax will begin to load
its components as soon as it is included in the page, and that will help speed
up the processing of the mathematics on your page.

Here, `path-to-MathJax` should be replaced by the URL for the main MathJax
directory, so if you have put the `MathJax` directory at the top level of you
server’s web site, you could use

```HTML
<script type="text/javascript" async src="/MathJax/MathJax.js?config=TeX-MML-AM_CHTML"></script>
```

to load MathJax in your page. For example, your page could look like

```HTML
<html>
    <head>
        ...
        <script type="text/javascript" async src="/MathJax/MathJax.js?config=TeX-MML-AM_CHTML"></script>
    </head>
    <body>
        ...
    </body>
</html>
```

<br><br>

## Update on delimiter configuration issue
---
Sometimes the so called "default delimiters" do not work properly. For example,
I tried the 'default 'in-line delimiter `\( ... \)`. It never works... It would
be safe to specify everything in the `<head>` session to ensure the delimiters
work properly.

```HTML
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    extensions: ["tex2jax.js"],
    jax: ["input/TeX", "output/HTML-CSS"],
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
      processEscapes: true
    },
    "HTML-CSS": { availableFonts: ["TeX"] }
  });
</script>
<script type="text/javascript"
  src="path-to-MathJax/MathJax.js">
</script>
```

_Note: `path-to-MathJax` in our case is an external url according to the 'CDN' method._

<br><br>

## Reference
---
`[1]` [MathJax Documentation Homepage](http://docs.mathjax.org/en/latest/start.html "MathJax Documentation Homepage") <br>
`[2]` [Loading and Configuring MathJax](http://docs.mathjax.org/en/latest/configuration.html#loading "Loading and Configuring MathJax") <br>
`[3]` [tex2jax configuration options](http://docs.mathjax.org/en/latest/options/tex2jax.html#configure-tex2jax "tex2jax configuration options") <br>
`[4]` [MathJax TeX and LaTeX Support](http://docs.mathjax.org/en/latest/tex.html#tex-support "MathJax TeX and LaTeX Support") <br>
