---
---

marp: true
theme: defalut
paginate: true
footer:

---

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>

# HTML
Prof. Dr.-Ing. Andreas Heil

![h:32 CC 4.0](../img/cc.svg)![h:32 CC 4.0](../img/by.svg) Licensed under a Creative Commons Attribution 4.0 International license. Icons by The Noun Project.

v1.0.0

---

# Objectives and Competencies 

---

# Markup Languages 

* Origin: _marking up_ documents
* Syntactical distinguishable from the text 
* Examples for markup languages 
    * LaTeX
    * XML
    * HTML
    * JSON? 

--- 

# JSON

> JSON is a text format that is completely language independent but uses conventions that are familiar to programmers of the C-family of languages, including C, C++, C#, Java, JavaScript, Perl, Python, and many others. These properties make JSON an ideal data-interchange language.[^1]

⏩ Eventually, JSON is not a markup language.

---

# HTML 

* **H**yper**t**ext **M**arkup **L**anguage
* Markup directives to describe content (structure, formatting)
* Declarative language 
* Annotation using tags `< >`
* Case-insensitive

Example 
```html
<p>Hello World!</p>
```

---

# Anatomy of HTML Tags

```plain
Opening tag     Closing tag
    ┌┴┐           ┌─┴─┐ 
    <p>Hello World</p>
       └────┬────┘
         Content
    └────────┬────────┘
          Element
```

```plain
    <p class="notes">Hello World</p>
       └─────┬─────┘
         Attribute
```

---

# Special Character 

| Literal character | Character Reference Equivalent |
| --- | --- |
| <	| \&lt; |
| >	| \&gt; |
| "	| \&quot; |
| '	| \&apos; |
| &	| \&amp; |
| nonbreaking space| \&nbsp; |

---

# HTML Document 

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>My HTML page</title>
  </head>
  <body>
    <p>Hello World!</p>
  </body>
</html>
```

---

# Header 

* Meta Tag

```html
<meta charset="utf-8">
```

* Link Tag

```html
<link rel="stylesheet" href="styles.css">
```

--- 

# XHTML 

* Extensible Hypertext Markup Language 
* Extended from XML and HTML
* More restrictive than vanilla HTML
* Why?
    * Malformed HTML (e.g. missing closing tags)

---

# XHTML Example 

```html
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
 "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
  <head>
    <title>My XHTML page</title>
  </head>
  <body>
    <p>Hello world!</p>
    <br />
  </body>
</html>
```

---

# Basic XHTML Rules 

* Every tag required a closing tag 
* Shorthand form for `<p></p>` is `<p />`
* Quotes are required for 
* `<html>`, `<head>`, `<title>`, and `<body>` are mandatory
* `<!DOCTYPE>` declaration is necessary at the top of the file
* No attribute minimization
* Elements and attributes must be in lowercases

---

# DOCTYPE 

* The `<!DOCTYPE>` declaration is **not** an HTML tag 
* Tells the browser what to expect, each doctype 
* HTML 4 and XHTML must refer to an DTD (Document Type Definition)
* HTML 5
`<!DOCTYPE html>`
* Different Doctypes allow different HTML tags

---

# References 

[^1]: https://www.json.org/



