#dev 

# Hyper Text Markup Language

> Html is skeleton/head of a website. CSS is skin/beauty. And JS is brain/functioning

Opening/closing tags OR empty tags

html is *case insensitive* language

`<!-- comments -->`

- `<link rel="stylesheet" href="style.css">` just before head ends
- `<p style="background-color: red;">` lorem `</p>` for internal css
- h1 to h6
- `<script src="script.js"></script>`
- `<a target="_blank" href="/linkedfile.html">` link name `</a>`
- unordered list `<ul>` (`<li>`): Types: disc, circle, square, none
- ordered list `<ol>` (`<li>`) types: 1, A, a, i, I
- definition list `<dl>` (`<dt>` and `<dd>`)
- table: caption, thead, tbody, tfoot: `<tr>` `<th>` `<td>`
- `<meta name="description" content="the actual description">`

# Search Engine Optimization
---

Website with better results and performance will be preferred by google
## Core Web Vitals:

#### Cumulative Layout Shift (CLS)
How much the page is shifting while loading
#### Largest Contextual Paint (LCP)
How fast is the largest/main element of a website loading
#### First Input Delay
How fast is the first interaction by user with a page responds

Might use lighthouse by google to check performance of a website
Responsive Website, resolution

# Forms
---

The `<form>` tag in HTML is used to create an HTML form for user input. It can contain various form elements like input fields, checkboxes, radio-buttons, submit buttons, reset etc., which are used to collect user input.

### Form for action
`<form action="URL">` inside body: URL is where the data will be submitted
method attribute = "get" or "post" defines how the data is send. post for bigger data

For inputting text in block:
placeholder shows hint to text entered
required attribute

```html
<label for="userid">*Enter your Username: </label>
<input type="text" id="userid" name="username" placeholder="your username" required>
```

For selecting Single Choice answer:
same name="gender" for only one correct answer
id and for, should be same for same tag to input when click on text

```html
<input type="radio" id="man" name="gender" value="male">
<label for="man">Male</label>
<input type="radio" id="women" name="gender" value="female">
<label for="women">Female</label>
```

don't prefer br tag. Use div to make them a block element

For Multiple correct answer:
same id for input-label pairs. and same name for every choice

```html
<div>
    <input type="checkbox" name="mcq" id="tom">
    <label for="tom">Extra tomato</label>
    <input type="checkbox" name="mcq" id="on">
    <label for="on">Extra onion</label>
    <input type="checkbox" name="mcq" id="lec">
    <label for="lec">Extra lettuce</label>
</div>
```

Textarea (comment/feedback/bio):
```html
<div>
    <label for="boxx">Give feedback:</label>
    <br> <!--CSS style later, don't use br tag-->
    <textarea name="comment" id="boxx" cols="30" rows="10"></textarea>
    <!--Bad practice to type inside text area-->
</div>
```

Select:
```html
<label for="lang">Your Preferred Language: </label>
<select name="language" id="lang">
    <option value="en">English</option>
    <option value="hi">Hindi</option>
    <option value="bn">Binary</option>
</select>
```

Autofocus attribute to move focus cursor to that text
Pattern for only accepted type of input. upper case/numbers etc.

### Fieldset
`<fieldset></fieldset>` can be used to group related forms together. Puts them in a nice black border box
`<legend>` can be used to add cool captions to fieldsets

```html
<fieldset>
    <legend>What your Gender?</legend>
    <input type="radio" id="male" name="gender" value="male">
    <label for="male">Male</label>
</fieldset>
```

# Inline and Block Elements
---

> **Inline elements don't start a new line and only take up as much width as necessary**

> **Block elements start a new line and take up entire width of their container**

## Block Elements (Most Commonly Used First)

- `<div>`: A generic container for flow content
- `<p>`: Paragraph
- `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, `<h6>`: Headings
- `<ul>`: Unordered list
- `<ol>`: Ordered list
- `<li>`: List item
- `<form>`: A section containing form controls
- `<table>`: Table
- `<section>`: A standalone section of a document
- `<header>`: A container for introductory content or navigational links
- `<footer>`: Footer of a section or page
- `<nav>`: A section containing navigation links
- `<article>`: A self-contained composition
- `<aside>`: Content indirectly related to main content
- `<main>`: The main content
- `<fieldset>`: Grouped form controls
- `<blockquote>`: Block quotation
- `<pre>`: Preformatted text
- `<canvas>`: For JavaScript graphics
- `<dl>`: Description list
- `<dt>`: Description term
- `<dd>`: Description details
- `<figure>`: Referenced content
- `<figcaption>`: Figure caption
- `<address>`: Contact information
- `<hr>`: Horizontal rule
- `<tfoot>`: Table footer

## Inline Elements (Most Commonly Used First)

- `<a>`: Anchor/link
- `<img>`: Image
- `<span>`: Generic inline container
- `<input>`: Input field
- `<label>`: Form label
- `<strong>`: Strong emphasis
- `<em>`: Emphasis
- `<br>`: Line break
- `<code>`: Code
- `<b>`: Bold
- `<i>`: Italic
- `<u>`: Underline
- `<small>`: Smaller text
- `<sub>`: Subscript
- `<sup>`: Superscript
- `<mark>`: Highlighted text
- `<q>`: Inline quote
- `<cite>`: Citation
- `<kbd>`: Keyboard input
- `<samp>`: Sample output
- `<var>`: Variable
- `<time>`: Time
- `<abbr>`: Abbreviation
- `<data>`: Machine-readable content
- `<acronym>`: Acronym (Not supported in HTML5)

## ID and Classes
---

> Id is a unique identifier for one element

> Class can be given to multiple elements for group styling

In CSS: `.class {}` and `#id{}`
IDs can also be used for linking

## Audio, Video And Media
---

```html
<video src="/Media/Sample/SampleVideo_1280x720_1mb.mp4" width="500" controls muted loop poster="/Media/Sample/woodcuts_16.jpg"></video>
```

Can also connect URL. autoplay. poster as thumbnail.

### Audio
src, controls, autoplay, loop, muted

Preload Attribute:
1. None - Default. No preloading. Only start downloading when interact
2. Metadata - browser only fetches metadata/details about audio
3. Auto - Browser fully preloads the audio

### SVG
To create high quality Images
Audio, Video, Img and SVG are all inline elements

```html
<svg height="100" width="100">
    <circle cx="50" cy="50" r="40" stroke="black" stroke-width="3" fill="red" />
</svg>
```

Can use externally by inputting in temp.svg
and use by ref img. Don't forget namespace attribute:

```html
<svg xmlns="http://www.w3.org/2000/svg"></svg>
```

### iFrames
Embed another HTML page in your website
Can embed websites and YouTube videos:

```html
<iframe src="https://www.codewithharry.com/" frameborder="0" height="500" width="500"></iframe>
```

## Semantic Tags
---
Semantic HTML elements like `<header>`, `<footer>`, `<article>`, and `<section>` clearly define their content, enhancing accessibility and SEO.

# Miscellaneous
---

### HTML Entities
Display reserved characters in HTML:

```html
&lt; for <
&gt; for >
&amp; for &
&nbsp; for non-breaking space
&copy; for ©
```

Can also use `<pre>` for preserving spaces and line breaks
`<blockquote>` for quotes
`<q>` for inline quotes
Obsolete tags like font, center are not used anymore

> And with that, we say goodbye to HTML and hello CSS~
