---
title: "CSS"
---

# CSS (Cascading Style Sheets)

CSS, or Cascading Style Sheets, is the magic behind the look and feel of websites. While HTML structures the content, CSS styles it, giving the web its visual appeal. Alongside HTML and JavaScript, CSS is a fundamental technology of the World Wide Web. It allows developers to keep the content separate from design, making web pages more flexible and easier to manage.

## A Bit of History

CSS was born in the mid-1990s to address the limitations of HTML in designing web pages. HTML was great for structuring content, but as websites grew more complex, there was a need for better design tools. Håkon Wium Lie, working with Tim Berners-Lee at CERN, proposed CSS in 1994, and it became an official W3C recommendation in 1996.

Over the years, CSS has evolved. CSS2 came out in 1998, and CSS3 followed in 1999, introducing new layout models, animations, transitions, and a modular specification approach for faster and more flexible development.

## CSS Basics

CSS uses a rule-based syntax to apply styles to HTML elements. A CSS rule consists of a selector and a declaration block. The selector identifies the HTML elements to style, and the declaration block contains one or more declarations, each with a property and a value.

### Basic Structure of a CSS Rule

```css
selector {
    property: value;
}
```

### Example

```css
h1 {
    color: blue;
    font-size: 24px;
}
```

Here, the `h1` selector targets all `<h1>` elements, setting the text color to blue and the font size to 24 pixels.

### How to Add CSS to HTML

You can apply CSS to HTML in three ways: inline styles, internal stylesheets, and external stylesheets.

#### Inline Styles

Inline styles are written directly within the HTML elements using the `style` attribute.

```html
<!DOCTYPE html>
<html>
<head>
    <title>Inline Styles Example</title>
</head>
<body>
    <h1 style="color: blue; font-size: 24px;">Hello, World!</h1>
</body>
</html>
```

#### Internal Stylesheets

Internal stylesheets are placed within the `<style>` tag inside the `<head>` section of the HTML document.

```html
<!DOCTYPE html>
<html>
<head>
    <title>Internal Stylesheet Example</title>
    <style>
        h1 {
            color: blue;
            font-size: 24px;
        }
    </style>
</head>
<body>
    <h1>Hello, World!</h1>
</body>
</html>
```

#### External Stylesheets

External stylesheets are separate CSS files linked to the HTML document using the `<link>` tag.

```html
<!DOCTYPE html>
<html>
<head>
    <title>External Stylesheet Example</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Hello, World!</h1>
</body>
</html>
```

`styles.css`:

```css
h1 {
    color: blue;
    font-size: 24px;
}
```

## Selectors

CSS selectors are patterns used to select the elements you want to style. There are various types of selectors, including element selectors, class selectors, ID selectors, and attribute selectors.

### Element Selectors

Element selectors target HTML elements based on their tag name.

```css
p {
    color: green;
}
```

### Class Selectors

Class selectors target elements based on their `class` attribute. Class names are prefixed with a dot (`.`).

```css
.intro {
    font-style: italic;
}
```

```html
<p class="intro">This is an introductory paragraph.</p>
```

### ID Selectors

ID selectors target elements based on their `id` attribute. IDs are prefixed with a hash (`#`) and must be unique within a document.

```css
#main {
    background-color: lightgray;
}
```

```html
<div id="main">This is the main content area.</div>
```

### Attribute Selectors

Attribute selectors target elements based on the presence or value of their attributes.

```css
a[target="_blank"] {
    color: red;
}
```

```html
<a href="https://www.example.com" target="_blank">External Link</a>
```

## The Cascade and Specificity

The term "cascading" in CSS refers to the way styles are applied to elements based on their order and specificity. When multiple rules target the same element, the cascade determines which rule takes precedence. Specificity is a measure of the importance of a rule, determined by the types of selectors used.

### Specificity Calculation

Specificity is calculated based on the following components:

1. Inline styles (highest specificity)
2. ID selectors
3. Class, attribute, and pseudo-class selectors
4. Element and pseudo-element selectors (lowest specificity)

```css
/* Example of specificity */
p {
    color: black; /* Lowest specificity */
}

.intro {
    color: blue; /* Higher specificity */
}

#main {
    color: green; /* Even higher specificity */
}

<style>
    <p id="main" class="intro" style="color: red;">This is the main paragraph.</p> <!-- Highest specificity due to inline style -->
</style>
```

## CSS Properties and Values

CSS provides a vast array of properties that can be used to control various aspects of the presentation, including layout, typography, colors, and more. Each property has a set of acceptable values, which can be keywords, lengths, percentages, colors, or other data types.

### Typography

Typography properties control the appearance of text, such as font family, size, weight, and style.

```css
body {
    font-family: 'Arial', sans-serif;
    font-size: 16px;
    font-weight: normal;
    font-style: italic;
    line-height: 1.5;
}
```

### Colors

Colors in CSS can be specified using various formats, including named colors, hexadecimal values, RGB, RGBA, HSL, and HSLA.

```css
h1 {
    color: #ff5733; /* Hexadecimal */
    background-color: rgb(255, 255, 255); /* RGB */
}

p {
    color: rgba(0, 0, 0, 0.5); /* RGBA */
    background-color: hsl(120, 100%, 50%); /* HSL */
}
```

### Box Model

The CSS box model is a fundamental concept that describes how elements are structured and displayed on a page. Each element is represented as a rectangular box, consisting of content, padding, border, and margin.

```css
div {
    width: 300px;
    padding: 20px;
    border: 5px solid black;
    margin: 10px;
}
```

### Example of the Box Model

```html
<!DOCTYPE html>
<html>
<head>
    <title>Box Model Example</title>
    <style>
        .box {
            width: 300px;
            padding: 20px;
            border: 5px solid black;
            margin: 10px;
            background-color: lightblue;
        }
    </style>
</head>
<body>
    <div class="box">This is a box model example.</div>
</body>
</html>
```

## Layout Techniques

CSS offers several layout techniques for designing complex web page layouts, including floats, positioning, Flexbox, and Grid.

### Floats

Floats are used to place elements side by side, typically for creating column-based layouts.

```css
.left {
    float: left;
    width: 50%;
}

.right {
    float: right;
    width: 50%;
}
```

### Example of Floating Elements

```html
<!DOCTYPE html>
<html>
<head>
    <title>Float Example</title>
    <style>
        .left {
            float: left;
            width: 50%;
            background-color: lightcoral;
        }

        .right {
            float: right;
            width: 50%;
            background-color: lightseagreen;
        }
    </style>
</head>
<body>
    <div class="left">Left Column</div>
    <div class="right">Right Column</div>
</body>
</html>
```

### Positioning

CSS positioning allows elements to be placed precisely within the layout, using properties like `position`, `top`, `right`, `bottom`, and `left`.

```css
.absolute {
    position: absolute;
    top: 50px;
    left: 100px;
}
```

### Example of Positioned Elements

```html
<!DOCTYPE html>
<html>
<head>
    <title>Positioning Example</title>
    <style>
        .container {
            position: relative;
            width: 400px;
            height: 200px;
            background-color: lightgray;
        }

        .absolute {
            position: absolute;
            top: 50px;
            left: 100px;
            width: 200px;
            height: 100px;
            background-color: lightblue;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="absolute">Positioned Element</div>
    </div>
</body>
</html>
```

### Flexbox

Flexbox is a powerful layout module that provides a more efficient way to align and distribute space among items in a container.

```

css
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.item {
    background-color: lightcoral;
    padding: 20px;
}
```

### Example of Flexbox Layout

```html
<!DOCTYPE html>
<html>
<head>
    <title>Flexbox Example</title>
    <style>
        .container {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .item {
            background-color: lightcoral;
            padding: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="item">Centered Item</div>
    </div>
</body>
</html>
```

### Grid

CSS Grid is a two-dimensional layout system that allows developers to create complex layouts with rows and columns.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 10px;
}

.item {
    background-color: lightseagreen;
    padding: 20px;
}
```

### Example of Grid Layout

```html
<!DOCTYPE html>
<html>
<head>
    <title>Grid Example</title>
    <style>
        .container {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            grid-gap: 10px;
        }

        .item {
            background-color: lightseagreen;
            padding: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="item">Item 1</div>
        <div class="item">Item 2</div>
        <div class="item">Item 3</div>
    </div>
</body>
</html>
```

## Responsive Design

Responsive design ensures that web pages look good on all devices, from desktops to smartphones. CSS media queries are used to apply different styles based on the screen size.

```css
/* Default styles */
body {
    font-size: 16px;
}

/* Larger screens */
@media (min-width: 600px) {
    body {
        font-size: 18px;
    }
}

/* Extra large screens */
@media (min-width: 1000px) {
    body {
        font-size: 20px;
    }
}
```

### Example of Responsive Design

```html
<!DOCTYPE html>
<html>
<head>
    <title>Responsive Design Example</title>
    <style>
        body {
            font-size: 16px;
        }

        @media (min-width: 600px) {
            body {
                font-size: 18px;
            }
        }

        @media (min-width: 1000px) {
            body {
                font-size: 20px;
            }
        }
    </style>
</head>
<body>
    <p>This text adjusts its size based on the screen width.</p>
</body>
</html>
```