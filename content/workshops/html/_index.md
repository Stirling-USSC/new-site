---
title: HTML Workshop
date: 2024-01-16
outputs: [Reveal]
---

<style>
code {
font-size: 0.8rem;
}
</style>

{{% section %}}

# Introduction

--------

## How Web Pages Work

The internet and its world-wide web has had a profound impact on all of our lives. It has put an unimagineably large
wealth of [mis]information at our fingertips, connected us to people on the other side of  the plannet, and
fundamentally changed how day-to-day business is conducted in the 21st century. But have you ever stopped to think about
how your browser is able to show you a complex, feature rich, and eye-catching page, seemingly out of the
ether?

---

### 1. Browser Requests Page

First, the browser looks up and connects to the server you're trying to access. It then asks the server for the specific
page you're trying to load, using the [HyperText Transfer Protocol (HTTP)][http], which is a specification of how the
messages between the web-browser and the web-server are structured. We'll be covering the HTTP protocol in much more
detail in a [later workshop][http-workshop].

[http]: <https://en.wikipedia.org/wiki/HTTP>
[http-workshop]: <https://github.com/stirling-ussc/http-workshop?usid=24&utid=5945885315>

---

### 2. Web Server Sends Response

The web-server then responds with instructions on how to build the page. There instructions are written in HTML, CSS,
and JavaScript, and these are the three technologies we will be teaching you how to write today.

--------

## The Roles of HTML, CSS and JavaScript

---

HTML

: Hypertext Markup Language

: Describes the structure and content of the webpage, such as sections, headings, paragraphs, etc.

---

CSS

: Cascading Style Sheets

: Provides a means to modify the appearance of the webpage, such as controlling layout, colours, and font styles.

---

JavaScript

: Allows interactivity on webpages by allowing website authors to run code within the user's browser.

{{% /section %}}

{{% section %}}

# HTML -- Describing Structure

--------

## Introduction

An essential component of any webpage, HTML allows you to describe the page's content, and overall structure.

---

All valid HTML documents have a set structure, shown below:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<!-- information about the document goes here -->
    <meta charset="UTF-8">
    <title>My Awesome Webpage</title>
</head>
<body>
    <!-- visible content goes here -->
</body>
</html>
```

--------

## Syntax

The syntax of HTML is almost identical to that of [XML][xml], though modern HTML5 is specified as a separate standard.
HTML is composed of:

[xml]: <https://en.wikipedia.org/wiki/XML>

* Comments
* Tags
* Tag attributes
* Static text

--------

### Comments

Comments in HTML are started by writing `<!--` and finished by writing `-->`. The browser ignores comments entirely,
they're useful for explaining your code to others, or even yourself. 😛

```html
<!-- This is a comment -->
<!-- comments can span multiple lines,
     like this -->
```

--------

### Tags

Tags are the fundamental building block of HTML. Each tag has a distinct name and purpose, for example, the `<title>`
tag allows you to specify the page's title (what appears on the tab):

```html
<title>My Awesome Site</title>
```

Tags are opened by writing `<tagname>`, and closed by writing `</tagname>`. 

---

#### Nesting Tags

Between the opening and closing tags, you can write static text, or nest other tags, like in the following example:

```html
<p>USCC is the <em>best</em> computer club!</p>
```

Here, the `<p>` tag denotes a paragraph, and `<em>` represents emphasised text (usually rendered as italics).

---

So the above HTML renders this:

USCC is the *best* computer club!

---

Some tags don't allow nested content, such as the `<link>` or `<br>` tags, so you don't need to close them. E.G:

```html
This is some text<br>with a line break in it.
```

This is some text\
with a line break in it.

--------

### Attributes

Some tags allow you to specify attributes (additional information used to render the tag). For example, you can specify the URL to navigate to when the user clicks a link:

```html
<a href="https://stirlingcomputer.club">USCC Website</a>
```

Here, the `<a>` tag creates an anchor (a link). `href` is the attribute name, and it has the
value `https://stirlingcomputer.club`. The displayed link text will be `USCC Website`. This code renders as:

[USCC Website](https://stirlingcomputer.club)

--------

### Static Text

Text can be placed anywhere inside the document, but how it's displayed depends on which tags surround it.

By default, whitespace in text is consolidated into a single space:

```html
<p>This     is a
test</p>
```

This is a test

--------

If you'd like to break a line early, use the `<br>` tag. If you'd like to specify the spacing yourself, use the `<pre>`
tag:

```html
<pre>
This is line 1
This        is line     2
</pre>
```

    This is line 1
    This        is line     2

--------

## Basic Structure

All modern HTML documents have this structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<!-- information about the document goes here -->
    <meta charset="UTF-8">
    <title>My Awesome Webpage</title>
</head>
<body>
    <!-- visible content goes here -->
</body>
</html>
```

---

1. `<!doctype html>`: specifies this is an HTML document
2. `<html lang="en">`: The `<html>` tag is the root tag, it surrounds all of the content. The `lang` attribute specifies
   the document language (`en` = English)
3. `<head>`: The `<head>` contains information about the document, much like a letter head or book's title page. Most of
   this content is not directly shown to the user, but is used by the browser to read the document correctly, fetch
   external resources such as style sheets and / or scripts, etc

---

4. `<meta charset="UTF-8">`: Sets the document's characterset to Unicode (UTF-8). This allows all unicode characters to
   be used in the document
5. ` <title>My Awesome Webpage</title>`: Sets the document title (displayed in the browser's title bar and / or tab)
6. `<body>`: Surrounds all visible content of the document. The majority of your content will go here

--------

## Common Head Tags

These tags should be placed in the `<head>` section of the document, and control how the browser reads and interprets
the HTML page:

---

1. #### `<title>`
   - Defines the title of the HTML document. It appears in the browser's title bar or tab.

2. #### `<meta charset="UTF-8">`
   - Specifies the character encoding for the document. UTF-8 is widely used and supports a broad range of characters.

---

3. #### `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
   - Sets the viewport properties, ensuring proper rendering on various devices by adjusting the initial zoom level.

4. #### `<meta name="description" content="Brief description of the page">`
   - Provides a concise description of the page's content, often displayed in search engine results.

---

5. #### `<meta name="keywords" content="HTML, web development, beginners">`
   - Lists keywords relevant to the page's content, helping search engines understand its context.

6. #### `<link rel="stylesheet" href="styles.css">`
   - Links an external CSS stylesheet to the HTML document, allowing for styling and layout adjustments.

---

7. #### `<style>`
    - Contains inline CSS styles for the document, allowing for specific styling without an external stylesheet.

8. #### `<link rel="icon" href="favicon.ico" type="image/x-icon">`
   - Specifies the favicon, a small icon displayed in the browser's address bar or tab.

---

9. #### `<link rel="canonical" href="https://example.com/canonical-url">`
   - Defines the canonical URL, indicating the preferred version of a page to search engines in case of duplicate content.

10. #### `<script src="script.js"></script>`
   - Links an external JavaScript file to the HTML document, providing dynamic functionality and interactivity. Without
   the `src` attribute, you can specify the JavaScript code inline, within the tag itself.

---

11. #### `<base href="https://example.com/">`
    - Sets the base URL for all relative URLs within the document, providing a reference point for resource links.

--------

## Body -- Defining the Page's Content

As noted earlier, the `<body>` contains the document's visible content.

--------

### Inline vs Block Elements

Some elements, like `<p>`, `<section`>`, and `<ul>` are considered "block elements". This means they cause a break in
the flow of the text. For example:

```html
This is a <p>test</p> of paragraphs.
```

This is a

test

of paragraphs.

---

Other elements, such as `<strong></strong>`, `<em></em>`, and `<u></u>` render inline (I.E. they don't interrupt the flow of text):

```html
I <em>love</em> writing <strong>HTML</strong> code!
```

I *love* writing **HTML** code!

---

## Common Body Tags

These `<body>` tags contribute to structuring and presenting content within the main body of an HTML document. Customize and combine them as needed for your specific web development projects.

--------

1. ### `<h1> to <h6>`
   - Header tags for defining headings. `<h1>` is the largest and `<h6>` is the smallest.

---

```html
<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>
<h4>Heading 4</h4>
<h5>Heading 5</h5>
<h6>Heading 6</h6>
```

<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>
<h4>Heading 4</h4>
<h5>Heading 5</h5>
<h6>Heading 6</h6>

--------

2. ### `<p>`
   - Defines a paragraph. Used to structure and separate blocks of text.

```html
<p>Paragraph 1</p>
<p>Paragraph 2</p>
```

<p>Paragraph 1</p>
<p>Paragraph 2</p>

--------

3. ### `<a href="https://example.com">Link Text</a>`
   - Creates a hyperlink to another web page or resource.

```html
Here is a <a href="https://stirlingcomputer.club">link to our website</a>.
```

Here is a <a href="https://stirlingcomputer.club">link to our website</a>.

--------

4. ### `<img src="image.jpg" alt="Description">`
   - Embeds an image in the document, with alternative text for accessibility.

```html
<img src="https://blindcomputing.org/logo/horizontal.png" alt="The Blind Computing logo">
```

<img src="https://blindcomputing.org/logo/horizontal.png" alt="The Blind Computing logo">

--------

5. ### `<ul>` and `<li>`
   - `<ul>` defines an unordered list, and `<li>` represents list items within it.

```html
<p>Shopping list</p>
<ul>
    <li>Milk</li>
    <li>Eggs</li>
    <li>Bread</li>
</ul>
```

<p>Shopping list</p>
<ul>
    <li>Milk</li>
    <li>Eggs</li>
    <li>Bread</li>
</ul>

--------

6. ### `<ol>` and `<li>`
   - `<ol>` defines an ordered list, and `<li>` represents list items with a specific order.

```html
<p>Todo list:</p>
<ol>
    <li>Learn HTML</li>
    <li>Learn CSS</li>
    <li>Publish website on Github Pages</li>
</ol>
```

<p>Todo list:</p>
<ol>
    <li>Learn HTML</li>
    <li>Learn CSS</li>
    <li>Publish website on Github Pages</li>
</ol>

--------

7. ### `<div>`
   - A generic container used for grouping and applying styles to a section of content.

```html
<div style="background-color: red; color: green;">
Some coloured text
</div>
```

<div style="background-color: red; color: green;">
Some coloured text
</div>

--------

8. ### `<span>`
   - Similar to `<div>`, but inline. Used for applying styles or scripting to a specific portion of text.

```html
The sky is very <span style="color: blue;">blue</span> today.
```

The sky is very <span style="color: blue;">blue</span> today.

--------

9. ### `<br>`
   - Inserts a line break, forcing text or elements following it to appear on a new line.

```html
There should only<br>
be three words<br>
on each line.
```

There should only<br>
be three words<br>
on each line.

--------

10. ### `<hr>`
    - Represents a horizontal rule, creating a visible separation between content sections.

```html
Page 1<hr>Page 2
```

Page 1<hr>Page 2

--------

11. ### `<form>`
    - Defines an HTML form for user input. Commonly used with input elements, such as text fields and buttons.

12. ### `<input type="text" placeholder="Enter text">`
    - Creates a text input field within a form.

13. ### `<button>`
    - Defines a clickable button, often used within forms to submit or reset data.

---

14. ### `<textarea rows="4" cols="50">Default text here</textarea>`
    - Generates a multiline text input area within a form.

---

### Example

```html
<form action="/update-profile" method="POST">
<label for="username-field">Username:</label>
<input type="text" id="username-field" placeholder="John Doe">

<label for="email-field">Email address:</label>
<input type="email" id="email-field" placeholder="john@example.com">

<label for="bio-field">Bio:</label>
<textarea id="bio-field" rows="5" columns="40"></textarea>

<button type="submit">Update profile</button>
</form>
```

---

<form action="/update-profile" method="POST">
<label for="username-field">Username:</label>
<input type="text" id="username-field" placeholder="John Doe">

<label for="email-field">Email address:</label>
<input type="email" id="email-field" placeholder="john@example.com">

<label for="bio-field">Bio:</label>
<textarea id="bio-field" rows="5" columns="40"></textarea>

<button type="submit">Update profile</button>
</form>

--------

15. ### `<iframe src="https://example.com" width="600" height="400"></iframe>`
    - Embeds an inline frame, allowing the display of another webpage within the current document.

```html
<iframe src="https://www.youtube.com/embed/gyIYQC5zuDQ" width="640" height="400"></iframe>
```

---

<iframe src="https://www.youtube.com/embed/gyIYQC5zuDQ" width="640" height="400"></iframe>

--------

16. ### `<table>`
   - Defines the beginning of a table.

17. ### `<tr>`
   - Represents a table row. Should be used within the `<table>` element.

18. ### `<th scope="row">`
   - Defines a header cell within a table. Typically used in the first row or column to label the content. The `scope`
     attribute specifies whether this is a row or column header for accessibility.

---

19. ### `<td>`
   - Represents a data cell within a table. Contains the actual content of the table.

20. ### `<thead>`, `<tbody>`, `<tfoot>`
   - `<thead>` groups header content in a table.
   - `<tbody>` groups the main content of the table.
   - `<tfoot>` groups footer content in a table.

21. ### `<caption>`
   - Adds a title or caption to a table. It should be placed immediately after the opening `<table>` tag.

---

### Example

```html
<table border="1">
  <caption>Employee Information</caption>
  <thead>
    <tr>
      <th>ID</th>
      <th>Name</th>
      <th>Position</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>John Doe</td>
      <td>Developer</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Jane Smith</td>
      <td>Designer</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Bob Johnson</td>
      <td>Manager</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="2">Total Employees</td>
      <td>3</td>
    </tr>
  </tfoot>
</table>
```

---

<table border="1">
  <caption>Employee Information</caption>
  <thead>
    <tr>
      <th scope="col">ID</th>
      <th scope="col">Name</th>
      <th scope="col">Position</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>John Doe</td>
      <td>Developer</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Jane Smith</td>
      <td>Designer</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Bob Johnson</td>
      <td>Manager</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="2">Total Employees</td>
      <td>3</td>
    </tr>
  </tfoot>
</table>

--------

## Structural Tags

These structural tags provide a semantic and meaningful way to structure the content of a webpage. By using these tags
appropriately, you enhance the readability, accessibility, and search engine optimization (SEO) of your HTML documents.

1. ### `<main>`
   - Represents the main content of the document. It should not contain content that is tangential or related to the site navigation.

---

2. ### `<header>`
   - Defines a header section usually containing the introductory content of a page, such as headings, logos, and navigation elements.

3. ### `<footer>`
   - Represents the footer of a section or page, typically containing metadata, copyright information, links to related pages, or contact details.

---

4. ### `<nav>`
   - Defines a navigation menu. It usually contains links to different sections or pages of the website.

5. ### `<article>`
   - Represents a self-contained piece of content that could be distributed and reused independently, such as a news article, blog post, or forum post.

---

6. ### `<aside>`
   - Represents content that is tangentially related to the content around it, such as a sidebar or a pull quote. It can also be used for content like related links or advertisements.

--------

# CSS -- Styling and Themeing Elements

--------

## Introduction

While HTML describes the *content* of the document and how it is *structure*ed, CSS tells your browser how to *style* said content.

--------

## Linking a Style Sheet in HTML

--------

## Syntax

CSS rules are laid out as follows --

```
<selector> {
    <directive> ;
    <directive> ;
    ...
    <directive> ;
}

<selector> {
    <directive> ;
    <directive> ;
}
```

and so on.

--------

## CSS Selectors

Each selector tells CSS *which* elements to apply the directives to. Selectors can be one of three *main* types - tag selectors, class selectors, and id selectors

---

<u>tag selectors</u> apply to *all* elements of a particular type. So we might, for example, have a CSS directive that applies to *all* `img` tags or *all* `h1` tags, and so on.

---

<u>class selectors</u> apply to all elements which have declared themselves to be part of a specific CSS class. So a CSS rule applying to `.someclass` would apply to *all* elements that have `class=someclass` in their HTML attributes

---

<u>id selectors</u> apply to one and only one element. A CSS rule for `#xyz` would apply *only* to the HTML element with `id=xyz` in its attributes

---

tag selectors are useful when you are sure that all elements of some type need some common formatting. For example, all `h1` elements should be of font xyz and of font-size n, etc.

---

class selectors are useful if there are multiple elements which need some common formatting, but are not all of the same element type. For example, we could have a rule that emphasises some text with a class selector of `.emphasis`. This allows us to emphasis text in any tag with a `class=emphasis` attribute, so this can be applied to `h1` *or* `a` *or* `p`, etc.

---

id selectors are useful when we want to apply *one-off* rules. So if we had, for example, a logo image in the header for our webpage which we wanted to show at a small resolution, we could set a `id=logoimg` in the `img` tag for *that particular* image and a CSS rule with a `#logoimg` selector; this ensures that the CSS rule applies to only that element *and* that we don't have to create entire class just for that one element.

---


The other kinds of CSS selectors are -

Adjacent sibling: `h2 + p`
    - Applies to all `p` elements that are siblings of `h2` elements in the HTML tree

Child: `li > ul`
    - Applies to all `ul` elements that are *directly* a child of an `li` element

Descendent: `ul a`
    - Applies to all `a` elements that are directly *or* indirectly the child of a `ul` element

---

There are many other CSS selectors covering more specific use cases, but the ones covered are the most used/important. For full details on CSS selectors refer to: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors

--------

## Common Properties

border:
    - The border property is used to create a border around an element on a webpage. You can specify the border width, style, and color.
    - `border: 2px solid #3498db`

---

fonts:
    - The font-family property sets the font for text on a webpage. You can specify multiple fonts in case the preferred one isn't available.
    - `font-family: 'Arial', sans-serif;`

---

background:
    - The background property sets the background color for an element on a webpage.
    - `background: #f2f2f2;`

---

background-image:
    - The background-image property sets an image as the background for an element.
    - `background-image: url('background.jpg');`

---

text-align:
    - The text-align property is used to set the horizontal alignment of text within an element.
    - `text-align: center;`

---

font-size:
    - The font-size property sets the size of the text within an element.
    - `font-size: 16px;`

---

width:
    - The width property sets the width of an element.
    - `width: 300px;`

---

height:
    - The height property sets the height of an element.
    - `height: 200px;`

--------

## CSS Colour Values

CSS `color`- properties can be set in multiple ways -

---

Hexadecimal:
    - Colors can be represented using a hexadecimal code, a combination of six characters (0-9 and A-F) representing Red, Green, and Blue values.
    - `color: #ff5733;`

---

RGB:
    - The RGB (Red, Green, Blue) model allows you to specify colors by indicating the intensity of each color component.
    - `color: rgb(255, 87, 51);`

---

Color Names:
    - CSS provides predefined color names, such as red, blue, or green, making it easy to use without memorizing codes.
    - `color: green;`

---

RGBA:
    - Similar to RGB, RGBA includes an Alpha channel to control the opacity of the color, ranging from 0 (transparent) to 1 (opaque).
    - `color: rgba(255, 0, 0, 0.5);`

--------

## Gradients

CSS gradients provide a smooth transition between two or more specified colors. They allow you to create beautiful backgrounds or apply color effects without using images.

There are several types of CSS gradients -

---

Linear Gradients:
    - A linear gradient creates a gradient effect along a straight line. You specify the starting and ending points, and the browser generates a smooth transition between the colors.

```css
.linear-gradient {
  background: linear-gradient(to right, #ff5733, #3498db);
}
```

---

Radial Gradients:
    - Radial gradients create a circular gradient effect, radiating from a center point to the outer edges. You can control the shape and size of the gradient.

```css
.radial-gradient {
  background: radial-gradient(circle, #ff5733, #3498db);
}
```

---

Color Stops:
    - Color stops allow you to define specific color points within the gradient. You can create more complex gradients by adding multiple color stops.

```css
.color-stops {
  background: linear-gradient(to right, #ff5733 20%, #3498db 50%, #2ecc71 80%);
}
```

---

Directional Gradients:
    - For linear gradients, you can specify the direction of the gradient using keywords like to right, to left, to bottom, to top, or angles like 45deg.

```css
.directional-gradient {
  background: linear-gradient(45deg, #ff5733, #3498db);
}
```

---

Repeating Gradients:
    - The repeating-linear-gradient and repeating-radial-gradient functions allow you to create a gradient pattern that repeats at regular intervals.

```css
.repeating-gradient {
  background: repeating-linear-gradient(45deg, #ff5733, #3498db 20%);
}
```

--------

## Spacing, Units

Pixels (px):
    - Pixels are a fixed unit of measurement. They provide a precise size, but they don't scale well on different devices.
    - `margin: 10px;`

Percentage (%):
    - Percentages are relative to the parent element's size. Useful for creating responsive designs.
    - `width: 50%;`

---

em:
    - The em unit is relative to the font-size of the element or its parent. It's great for maintaining scalability in responsive designs.
    - `padding: 2em;`

rem:
    - Similar to em, but relative to the root element's font-size. It ensures consistent scaling across the entire page.
    - `margin: 1rem;`

--------

## Positioning With position/margin/padding

padding:
    - The padding property adds space inside the boundaries of an element. It helps control the spacing between the content and the border of the element.
    - `padding: 10px;`

margin
    - The margin property adds space outside the boundaries of an element. It controls the spacing between the element and its neighboring elements.
    - `margin: 20px;`

---

position
    - The position property determines how an element is positioned on a webpage. It can be set to relative, absolute, fixed, or static.
    - `position: relative;`

--------

## Basic Layout with CSS Flexbox

Flexbox, short for Flexible Box, is a layout model in CSS that allows you to design complex layouts more efficiently and with less code. It provides a way to distribute space and align items within a container, even when their size is unknown or dynamic.

---

To use Flexbox, you first designate a container as a flex container by applying display: flex; to it. This property turns all direct children of the container into flexible items.

```css
.flex-container {
  display: flex;
}
```

---

The flex-direction property defines the direction in which the flex items are placed in the flex container. It can be set to row, column, row-reverse, or column-reverse.

```css
.flex-container {
  display: flex;
  flex-direction: row; /* or column, row-reverse, column-reverse */
}
```

---

The align-items property aligns flex items along the cross-axis. It can be set to flex-start, flex-end, center, stretch, or baseline.

```css
.flex-container {
  display: flex;
  align-items: center; /* or flex-start, flex-end, stretch, baseline */
}
```

---

The justify-content property aligns flex items along the main axis. It can be set to flex-start, flex-end, center, space-between, space-around, or space-evenly.

```css
.flex-container {
  display: flex;
  justify-content: space-between; /* or flex-start, flex-end, center, space-around, space-evenly */
}
```

---

Each child element of a flex container becomes a flex item. You can adjust the size of flex items using properties like flex-grow, flex-shrink, and flex-basis.

```css
.flex-item {
    flex: 1; /* shorthand for flex-grow, flex-shrink, and flex-basis */
}
```

--------

# Publishing Your Website

--------

## Github Pages

--------

## Creating a Repository

* Go to <https://github.com>, sign in and click "new" followed by "new repository"
* Name your repository `<username>.github.io`, for example, my username is `mcb2003`, so my repo is called
  `mcb2003.github.io`
* Choose to create a public repository, and add a README
* Click "create repository"

--------

## Commit Your Code

* On your new repository's home page, click "creating a new file"
* Name your file "index.html" (this is the default name for the homepage of your site
* Paste your code into the file, then click "commit changes"
* Modify the commit message if you'd like, then click "commit changes" once again

--------

## Enable Github Pages

Now we will teach you how to [Create a GitHub pages site](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site).
This lets you publish your website on the internet using GitHub pages to host it.

---

To create a GitHub pages site for your website you must have a public repository containing the files you're website is made from.

GitHub will looks for the index.html (or index.md or README.md) file of your website to use as the entry file for your site. You must include the site entry file at the top of the repository directory or at the top level of the directory which you have set as the source directory.

---

Right. Now, how to create a GitHub pages site for your website from your GitHub repository for your website?
 1. go to your repo
 2. go to the setting tab
 3. go to the **pages** section under **code and automation** in the settings tab
 4. leave source as deploy from branch
 5. select the main branch or whichever branch of your repo you want your website to be built from
 6. click save
 7. wait a few minutes for your website to publish

--------

## View Your site!

{{% /section %}}
