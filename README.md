# Coding Standards & Guidelines

These standards and guidelines are mainly for CrystalCommerce front-end client projects and frameworks.

## Table of Contents

  1. [General](#general)
  1. [HTML & Liquid](#html)
  1. [CSS](#css)
  1. [Javascript](#arrays)
  1. [Performanace](#perf)
  1. [SEO & Data](#seo)
  1. [More Resources](#moreresources)

### <a name='general'>General</a>

- **Spaces not Tabs**: Use spaces when coding and not tab characters. Use 4 spaces for a tab.

    *Good*
    ```html
    <div class="container">
        <p>This is my text</p>
    </div>
    ```

    *Bad*
    ```html
    <div class="container">
      <p>This is my text</p>
    </div>
    ```

- Edit [humans.txt](https://github.com/crystalcommerce/Heisenberg/blob/master/humans.txt) to include the designers, dev's and clients name of the project

### <a name='html'>HTML & Liquid</a>

- **HTML 5 Doctype**: Use the HTML 5 doctype at the top of your website

    *Good*
    ```html
    <!DOCTYPE html>
    ```

    *Bad*
    ```html
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
    "http://w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    ```

- **HTML5 Markup**: Use HTML5 markup syntax

    *Good*
    ```html
    <header><!-- my header --></header>
    ```

    *Bad*
    ```html
    <div class="header"><!-- old way to do headers --></div>
    ```

- **Tables**: Tables should NOT be used for layout design. Use CSS.

- **Comments**
    - Limit the use of rendered comments for production (js & css comments get removed/ minified)
    - don't use "end div" comments. Use the inspector and dev tools to debug html/ css
    - comments should be implemented with liquid syntax
    - Use liquid comments instead of HTML comments when possible

    *Good*
    ```liquid
    {% comment %} This comment does NOT show on the rendered source {% endcomment %}

    {% comment %}

        This is a multiline comment that can
        be used to explain in more detail

    {% endcomment %}

    ```

    *Bad*
    ```html
    <!-- My Comments Here -->

    <div class="container">

    </div><!-- end container -->
    ```
- **Minimum DOM Size**: Keep the dom size to a minimum and don't use unnecessary elements

    *Bad*
    ```html
    <div class="wrapper">
        <div class="inner">
            <div class="content">
                <p>This is unnecessary</p>
            </div>
        </div>
    </div>
    ```

    *Good*
    ```html
    <div class="content">
        <p>This is better</p>
    </div>
    ```

- **Asset URL**: Use the asset_url for including images and other assets
    - `asset_url` returns asset path relative to the current theme’s asset dir on the cdn

    *Bad*
    ```liquid
    <img src="files/assets/myimage.jpg">
    ```

    *Good*
    ```liquid
    <img src="{{ "myimage.jpg" | asset_url }}">
    ```

    *Output*
    ```liquid
    <img src="http://cdn2.crystalcommerce.com/themes/clients/MyClient/assets/myimage.jpg">
    ```

- **Config.yml**: Use the `config.yml` to include CSS & JS
    - The config.yml will minify concatenate JS & CSS into fewer files.
    - [More info at docs.cc.com](http://docs.crystalcommerce.com/features/theme_config.html)

    ```liquid
    {% comment %} This minifies the CSS by setting it to false {% endcomment %}
    {{ "head" | css_minify_tag: false }}
    ```

- Use <label> fields to label each form field. The for attribute should associate itself with the input field, so users can click the labels and obtain focus.

### <a name='css'>CSS</a>

- CSS3 should be used over images, when applicable *(example, rounded corners, gradiants etc)*
- **Custom CSS**: use `custom.global.css` for all your custom CSS
- **Responsive CSS**: use `custom.devices.css` for your responsive CSS
- All CSS rules should have a space after the selector colon and a trailing semi-colon.
- 0 value requires no units

    *Bad*
    ```css
    .my-div {
        margin: 0px;
    }
    ```

    *Good*
    ```css
    .my-div {
        margin: 0;
    }
    ```

- **IDs and Class names**: the use of IDs is not allowed in CSS and should only be used for Javascript

    *Bad*
    ```css
    #my-div {background: blue;}
    ```

    *Good*
    ```css
    .my-div {background: blue;}
    ```


- **CSS Hacks**: any CSS hacks should be written in `custom.shame.css` and should be well commented on why you are using the hack

    *Bad*
    ```css
    /* custom.global.css */

    #page-container {background: #000 !important;}
    ```

    *Good*
    ```css
    /* custom.shame.css */

    /*  Page container gets overwritten by Javascript
        so I need to overwrite it with !important   */
    #page-container { background: #000 !important;}
    ```

- **Selectors**: CSS selectors should not exceed 3 levels deep
    - If a selector needs to exceed 3 levels, use sparingly

    *Bad*
    ```css
    .content .product-container .product .inner .name {
        font-weight: bold;
    }
    ```

    *Good*
    ```css
    .product-container .product .name {
        font-weight: bold;
    }
    ```

*Work in progress*

General:
- use normalize.css if reset is not present

Presentation Considerations:
- do not nest styles with indentation
- group browser prefixes, separate with line breaks
- w3c css3 spec should be listed last
- css properties should be alphabetized
- sections of css should labeled with a comment head
- comment heads should be prefixed with an underscore i.e:
- "_HEADER MAIN STYLES"
- include table of contents (list of comment heads)
- see example...

Images:
- image sprites should be used when CSS3 styles are not appropriate
- use as few images as possible
- image sprites should be called only once
- this should be near the top of your stylesheet
- you can use a .sprite class to make this easier
- use sprites for hover effects at all costs


### <a name='javascript'>Javascript</a>

*Work in progress*


### <a name='perf'>Perfomance</a>

- **HTTP Requests**: Minimize the amount of requests to the page by minifiying CSS & JS. You can have the server minify files with the use of config.yml
- **non-blocking Javascript**: Make sure javascript is loaded at the bottom of the page and the page markup is rendered first. Javascript can block the page load causing a longer loading times.
- **Google Fonts**: You can include multiple Google Web Fonts with one `<link>` tag. This limits the amount of requests to their server to 1. <sup>[Refrence](https://developers.google.com/fonts/docs/getting_started#Syntax)</sup>

    *Good*
    ```html
    <link href='http://fonts.googleapis.com/css?family=Open+Sans|Roboto' rel='stylesheet' type='text/css'>
    ```

    *Bad*
    ```html
    <link href='http://fonts.googleapis.com/css?family=Open+Sans' rel='stylesheet' type='text/css'>
    <link href='http://fonts.googleapis.com/css?family=Roboto' rel='stylesheet' type='text/css'>
    ```


- ......


### <a name='seo'>SEO & Data</a>

- **Schema Data**: Use schema data when applicable. You can test the data with [Google's Structured Data Testing Tool](http://www.google.com/webmasters/tools/richsnippets). More info at [Schema.org](http://schema.org)

    *Good*
    ```html
    <div class="product" itemscope itemtype="http://schema.org/Product">

        <h5 class="name" itemprop="name">My Product</h5>

        <div itemprop="offers" itemscope itemtype="http://schema.org/Offer">

            <span class="price" itemprop="price" content="5.99">$5.99</span>

        </div>

        <a href="/product">
            <img src="product.jpg" alt="My Product" />
        </a>

    </div>
    ```

    *Bad*
    ```html
    <div class="product">

        <h5 class="name">My Product</h5>
        <span class="price">$5.99</span>

        <a href="/product">
            <img src="product.jpg" alt="My Product" />
        </a>

    </div>
    ```

### <a name='moreresources'>External Resources</a>

- [View more resources](https://github.com/crystalcommerce/Heisenberg/wiki/External-Resources)
- [TMW Front-end guidelines](https://github.com/tmwagency/TMW-frontend-guidelines/blob/master/Front-End%20development%20guidelines.mdown)
