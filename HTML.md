### *HyperText Markup Language* is skeleton/head of a website. Css is skin/beauty. And JS is brain/functioning

Opening and closing tags, or empty tags
### html is case insensitive language

 <! - - comments- - >

- <link rel = “stylesheet” href=”style.css”> just before head ends
- <p style”background-color: red;”> lorem </p> for internal css
- h1 to h6,
- <script scr=”script.js”> </script>
- <a target = “_blank” (for open link in new tab) href =”/linkedfile.html”> link name </a>
- unordered list <ul> (<li>): Types : disc, circle, square, none
- ordered list <ol> (<li>) types : 1, A, a, i, I
- definition list <dl> (<dt> and <dd>)
- table : caption, thead, tbody, tfoot :  <tr> <th> <td>
- <meta name=”description” content=”the actual description”>

---

## Search Engine Optimization

Website with better results and performance will be prefers by google

## Core Web Vitals:

### Cumulative Layout Shift (CLS)

How much the page is shifting while loading

### Largest Contextual Paint (LCP)

how fast is the largest/main element of a website loading

### First Input Delay

How fast is the first interaction by user with a page responds

Might use lighthouse by google to check performance of a website

Responsive Website, resolution

---

# Forms

The `<form>` tag in HTML is used to create an HTML form for user input. It can contain various form elements like input fields, checkboxes, radio-buttons, submit buttons,reset etc., which are used to collect user input.

### Form for action

<form action="URL"> inside body : URL is where the data will be submitted

method attribute = “get” or “post” defines how the data is send. post for bigger data

For inputting text in block

placeholder shows hint to text entered

required attribute

```html
        <label for="userid">*Enter your Username: </label>
        <input type="text" id="userid" name="username" placeholder="your username" required>
```

For selecting Single Choice answer

same name=”gender” for only one correct answer

id and for, should be same for same tag to input when click on text

```html
    <input type="radio" id="man" name="gender" value="male">
    <label for="man">Male</label>
    <input type="radio" id="women" name="gender" value="female">
    <label for="women">Female</label>
```

don’t prefer br tag. Use div to make them a block element

For Multiple correct answer

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

Textarea (comment/feedback/bio)

```html
    <div>
        <label for="boxx">Give feedback:</label>
        <br> <!--CSS style later, don't use br tag-->
        <textarea name="comment" id="boxx" cols="30" rows="10"></textarea>
        <!--Bad practice to type inside text area-->
    </div>
```

Select

```html
        <label for="lang">Your Preferred Language: </label>
        <select name="language" id="lang">
            <option value="en">English</option>
            <option value="hi">Hindi</option>
            <option value="bn">Binary</option>
        </select>
```

Autofocus attribute to move focus curson to that text

Pattern for only accepted type of input. upper case/numbers etc.

### Fieldset

<fieldset></..> can used to group related forms together. Puts them in a nice black border box

<legend> can be used to add cool captions to fieldsets

```html
        <fieldset>
            <legend>What your Gender?</legend>
            <input type="radio" id="male" name="gender" value="male">
            <label for="male">Male</label>
        </fieldset>
```

---

# Inline and Block Elements

> **Inline elements don’t start a new line and only take up as much width as necessary**
> 

> **Block elements start a new line and take up entire width of their container**
> 

## Block Elements (Most Commonly Used First)

- `<div>`: A generic container for flow content.
- `<p>`: Paragraph.
- `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, `<h6>`: Headings.
- `<ul>`: Unordered list.
- `<ol>`: Ordered list.
- `<li>`: List item.
- `<form>`: A section containing form controls.
- `<table>`: Table.
- `<section>`: A standalone section of a document.
- `<header>`: A container for introductory content or a set of navigational links.
- `<footer>`: Footer of a section or page.
- `<nav>`: A section of a page that contains navigation links.
- `<article>`: A self-contained composition in a document.
- `<aside>`: A section of a page that contains information indirectly related to the main content.
- `<main>`: The main content of a document.
- `<fieldset>`: A set of form controls grouped under a common name.
- `<blockquote>`: A block of text that is a quotation from another source.
- `<pre>`: Preformatted text.
- `<canvas>`: A container used to draw graphics via JavaScript.
- `<dl>`: Description list.
- `<dt>`: Term in a description list.
- `<dd>`: Description in a description list.
- `<figure>`: Any content that is referenced from the main content.
- `<figcaption>`: A caption for a `<figure>` element.
- `<address>`: Contact information for the author or owner of the document.
- `<hr>`: A thematic break or a horizontal rule.
- `<tfoot>`: Footer of a table.

## Inline Elements (Most Commonly Used First)

- `<a>`: Anchor or hyperlink.
- `<img>`: Image.
- `<span>`: Generic inline container.
- `<input>`: Input field.
- `<label>`: Label for a form element.
- `<strong>`: Strong emphasis.
- `<em>`: Emphasized text.
- `<br>`: Line break.
- `<code>`: Code snippet.
- `<b>`: Bold text.
- `<i>`: Italic text.
- `<u>`: Underlined text.
- `<small>`: Smaller text.
- `<sub>`: Subscript.
- `<sup>`: Superscript.
- `<mark>`: Marked or highlighted text.
- `<q>`: Short inline quotation.
- `<cite>`: Citation.
- `<kbd>`: Keyboard input.
- `<samp>`: Sample output.
- `<var>`: Variable in a mathematical expression or programming context.
- `<time>`: Time.
- `<abbr>`: Abbreviation.
- `<data>`: Machine-readable translation of content.
- `<acronym>`: Acronym (Not supported in HTML5).

---

## ID and Classes

> Id is an attribute, a unique identifier assigned to only one element for unique styling and JavaScript manipulations
> 

> Class attribute can be given to group of elements at once, to easily change their looks and behavior. Not unique. An element can also have multiple elements.
> 

In CSS .class {} and #id{}

ID’s can also be used for linking

---

## Audio, Video And Media

```html
<video src="/Media/Sample/SampleVideo_1280x720_1mb.mp4" width="500" controls muted loop poster="/Media/Sample/woodcuts_16.jpg"></video>
```

Can also connect URL. autoplay. poster as thumbnail.

### Audio

scr, controls, autoplay, loop, muted

Preload Attribute: 

1. None - Default. No preloading. Only start downloading when interact
2. Metadata - browser only fetches the metadata/details about the audio. Mainly to display duration without fully loading
3. Auto - Browser fully preloads the audio while trying to avoid delaying other important parts of website. 

### SVG

To create high quality Images

Audio, Video, Img and SVG are all inline elements

```html
<svg height="100" width="100">
    <circle cx="50" cy="50" r="40" stroke="black" stroke-width="3" fill="red" />
</svg>
```

Can use externally by inputting in a temp.svg

and use by ref img. Don’t forgot to declare namespace attribute

```html
<svg xmlns="<http://www.w3.org/2000/svg>"></svg>
```

### iFrames

They allow to to embed another HTML page in your website

You can embed different websites, and even YouTube videos. By sharing, embed and pasting.

```html
<iframe src="<https://www.codewithharry.com/>" frameborder="0" height="500" width="500"></iframe>
```

---

## Semantic Tags

Semantic HTML elements like `<header>`, `<footer>`, `<article>`, and `<section>` clearly define their content, enhancing accessibility and SEO. For instance, `<header>` contains introductory,  `<nav>` navigational content, `<footer>` is for footers, `<article>` encloses self-contained content, and `<section>` is for standalone sections in an HTML document. Similarly, <aside>, <figure>, <time>, etc.

---

# Miscellaneous

### HTML Entities

They allow you to display reserved characters in html. Example to display <p>, extra spaces, math symbols.

```html
&lt; for <
&gt; for >
&amp; for &
&nbsp; for non-breaking span
&copy; for ©
```

Can also use `<pre> to show extra spaces   and enters </pre>`

<blockquote> for quotes

<q> for inline quotes

Obsolete tags like font, center are not used anymore. As modern css is much better

> And with that, we say goodbye to HTML and hello CSS~
>