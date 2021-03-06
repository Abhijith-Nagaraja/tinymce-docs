---
layout: default
title: 10. Filter Content
description: Learn how to create clean, maintainable and readable content.
---

TinyMCE has comprehensive content filtering capabilities. These settings change the way the editor handles the input and output of content, helping your users create clean, maintainable and readable content.

These settings enable developers to control content styling features that are available to users such as font formats, font sizes, and text indentation. It is these type of customizations we will focus on here by looking at 1 of the 32 content filtering options available to developers.

There are of course many configuration options dealing with complex parsing of text. However, most of these are quite advanced and outside the scope of this Get Started guide. Check out the [Content Filtering]({{ site.baseurl }}/configure/content-filtering/) section to learn more.


## Role your own style formats

In this section of the guide we will look at the [formats]({{ site.baseurl }}/configure/content-filtering/#font_formats) configuration option, which enables developers to override TinyMCE defaults and add custom "formats" to the editor.

A format is the style that gets applied to text when a user presses the bold button inside the editor. TinyMCE is equipped with a text formatter engine that enables you to specify exactly what it should produce when a user clicks the bold button for example.

### Style merging

> Pro tip: similar elements and styles will be merged by default to reduce the output HTML size. So for example, if you select a word and select a font size and font face for it, it will merge these two styles into one `span` element instead of one `span` for **each format type**.

### Built in formats

TinyMCE has some built in formats that you can override. You may recall some of these from the default controls we mentioned in the [Basic Setup](../basic-setup) part of this Get Started guide:

* alignleft
* aligncenter
* alignright
* alignfull
* bold
* italic
* underline
* strikethrough
* forecolor
* hilitecolor
* fontname
* fontsize
* blockquote
* removeformat
* p
* h1, h2, h3, h4, h5, h6
* div
* address
* pre
* div
* code
* dt, dd
* samp

Some built in formats `fontsize`, `fontname`, `forecolor`, `hilitecolor` use a variable in their definition named `%value`. This one gets replaced with the user selected item such as a color value. Check the variable substitution section below for details.

### Format parameters

Before we move on to the table of format parameters below, we want to acknowledge that this content is starting to get a little more advanced. Since you've made it this far and we think you can handle it.

| Name       | Summary          |
|------------|------------------|
| inline     | Name of the inline element to produce, for example, `span`. The current text selection will be wrapped in this inline element.
| block      | Name of the block element to produce for example `h1`. Existing block elements within the selection gets replaced with the new block element. |
| selector   | CSS 3 selector pattern to find elements within the selection by. This can be used to apply classes to specific elements or complex things like odd rows in a table. |
| classes    | Space separated list of classes to apply the selected elements or the new inline/block element. |
| styles     | Name/value object with CSS style items to apply such as color etc. |
| attributes | Name/value object with attributes to apply to the selected elements or the new inline/block element. |
| exact      | Disables the merge similar styles feature when used. This is needed for some CSS inheritance issues such as text-decoration for underline/strikethrough. |
| wrapper    | State that tells that the current format is a container format for block elements. For example a div wrapper or blockquote. |

### Example of usage of the formats option

This example overrides some of the built-in formats and tells TinyMCE to apply classes instead of inline styles. It also includes a custom format that produced `h1` elements with a title attribute and a `red` `css` style.

```js
// Output elements in HTML style
tinymce.init({
  selector: 'textarea',  // change this value according to your html
  formats: {
    alignleft: {selector : 'p,h1,h2,h3,h4,h5,h6,td,th,div,ul,ol,li,table,img', classes : 'left'},
    aligncenter: {selector : 'p,h1,h2,h3,h4,h5,h6,td,th,div,ul,ol,li,table,img', classes : 'center'},
    alignright: {selector : 'p,h1,h2,h3,h4,h5,h6,td,th,div,ul,ol,li,table,img', classes : 'right'},
    alignfull: {selector : 'p,h1,h2,h3,h4,h5,h6,td,th,div,ul,ol,li,table,img', classes : 'full'},
    bold: {inline : 'span', 'classes' : 'bold'},
    italic: {inline : 'span', 'classes' : 'italic'},
    underline: {inline : 'span', 'classes' : 'underline', exact : true},
    strikethrough: {inline : 'del'},
    forecolor: {inline : 'span', classes : 'forecolor', styles : {color : '%value'}},
    hilitecolor: {inline : 'span', classes : 'hilitecolor', styles : {backgroundColor : '%value'}},
    custom_format: {block : 'h1', attributes : {title : 'Header'}, styles : {color : 'red'}}
  }
});
```


### Power user bonus

> This probably shouldn't be in a Get Started guide, but we wanted to show you an example of the type of configuration options you'll find in the [Content Filtering]({{ site.baseurl }}/configure/content-filtering/) configuration docs. Plus it's something you may need to do someday.

The `schema` option enables you to switch between the HTML4 and HTML5 schema. This controls the valid elements and attributes that can be placed in the HTML. This value can either be the default `html5`, `html4` or `html5-strict`.

The `html5` schema is the full HTML5 specification including the older HTML4 elements for compatibility. The `html5-strict` schema will only allow the elements in the current HTML5 specification, excluding things that were removed. The `html4` schema includes the full HTML4 transitional specification.

```js
tinymce.init({
  selector: 'textarea',  // change this value according to your html
  schema: 'html5'
});
```

{% assign_page next_page = "/get-started/localize-your-language/index.html" %}
{% include next-step.html next=next_page %}
