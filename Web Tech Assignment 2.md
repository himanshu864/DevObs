# ***Name***: Himanshu Aggarwal
# ***Roll No***: 2K20/CO/198

## **Assignment-01:** HTML Tags for Text Formatting
---

### 1. **Superscript: `<sup>` Tag**

- The `<sup>` tag is used to make text appear smaller and slightly higher than the normal text. This is commonly used for displaying exponents or ordinal numbers.

**Example:**
```html
<p>This is the formula for water: H<sub>2</sub>O.</p>
<p>E = mc<sup>2</sup></p>
```

### 2. **Subscript: `<sub>` Tag**

- The `<sub>` tag is used to make text appear smaller and slightly lower than the baseline. This is often used for chemical formulas and mathematical indices.

**Example:**
```html
<p>CO<sub>2</sub> is a greenhouse gas.</p>
```

### 3. **Strikethrough: `<s>` or `<del>` Tag**

- The `<s>` tag or the `<del>` tag can be used to add a strikethrough effect to text. `<del>` is generally used to indicate deleted content.

**Example:**
```html
<p>Old price: <s>$100</s> New price: $80</p>
<p>This statement is <del>incorrect</del> revised.</p>
```

### 4. **Super Bold: Using `<b>` with CSS for Enhanced Bold**

- While `<b>` provides bold text, "super bold" can be achieved by adding CSS `font-weight` property for greater emphasis. HTML doesn’t have a dedicated "super bold" tag, so this needs to be customized with CSS.

**Example:**
```html
<p>This text is <b style="font-weight: 900;">super bold</b>.</p>
```

### 5. **Underline Without `<u>` Tag (Using CSS)**

- Instead of the deprecated `<u>` tag, CSS can be used to apply an underline effect to text.

**Example:**
```html
<p>This text is <span style="text-decoration: underline;">underlined</span></p>
```


# **Assignment-02:** Design a Webpage with Links
---

Let's create a basic HTML file (`index.html`) that includes links to internal pages, external pages, and an image link.

#### Main HTML File (`index.html`)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Webpage with Links</title>
  </head>
  <body>
    <h1>Webpage with Various Links</h1>

    <ul>
      <li><a href="internal.html">Linking Web Pages Internally</a></li>
      <li>
        <a href="https://www.example.com" target="_blank"
          >Linking Web Pages Externally</a
        >
      </li>
      <li><a href="image_link.html">Using Image as a Link</a></li>
    </ul>
  </body>
</html>
```

#### Internal Links Page (`internal.html`)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Internal Links</title>
  </head>
  <body>
    <h2>Internal Links Page</h2>
    <ul>
      <li><a href="#section1">Go to Section 1</a></li>
      <li><a href="#section2">Go to Section 2</a></li>
    </ul>

    <h3 id="section1">Section 1</h3>
    <p>This is the content of section 1.</p>

    <h3 id="section2">Section 2</h3>
    <p>This is the content of section 2.</p>
  </body>
</html>
```

#### Image as Link Page (`image_link.html`)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Image Links</title>
  </head>
  <body>
    <h2>Using Image as a Link</h2>

    <!-- Single link with image -->
    <p>
      <a href="https://www.example.com">
        <img src="example-image.jpg" alt="Example Image Link" width="200" />
      </a>
    </p>

    <!-- Multiple links with a single image -->
    <p>
      <map name="image-map">
        <area
          shape="rect"
          coords="0,0,100,100"
          href="https://www.example.com/page1"
          alt="Page 1"
        />
        <area
          shape="rect"
          coords="100,0,200,100"
          href="https://www.example.com/page2"
          alt="Page 2"
        />
      </map>
      <img
        src="example-image.jpg"
        usemap="#image-map"
        alt="Example Image with Multiple Links"
        width="200"
      />
    </p>
  </body>
</html>
```

### **Explanation:**

- **Internal Links:** The `internal.html` page uses anchor links to navigate within the same page.[]()
- **External Links:** The main HTML file (`index.html`) includes an external link that opens in a new tab using `target="_blank"`.
- **Image Links:** The `image_link.html` page contains:
    - A single clickable image.
    - A single image mapped with multiple clickable areas using `<map>` and `<area>` tags for navigation.

