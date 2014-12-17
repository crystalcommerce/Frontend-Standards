# Coding Standards & Guidelines

These standards and guidelines are mainly for CrystalCommerce front-end client projects and frameworks.

## Table of Contents

  1. [General](#general)
  1. [HTML & Liquid](#html)
  1. [CSS](#css)
  1. [Javascript](#arrays)
  1. [Performance](#perf)
  1. [SEO & Data](#seo)
  1. [More Resources](#moreresources)

### <a name='general'>General</a>

- **Spaces not Tabs**
    - Use spaces when coding and not tab characters. Use 4 spaces for a tab.

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
    
    - In Sublime Text you can see tabs vs spaces if you highlight the code area
  
    ![Imgur](http://i.imgur.com/w78CPQb.png)

- **Attribution**
    - Edit [humans.txt](https://github.com/crystalcommerce/Heisenberg/blob/master/humans.txt) to include the designer, dev and client names for the project. [Read about the robots.txt initiative.](http://humanstxt.org/)

### <a name='html'>HTML & Liquid</a>

- **HTML 5 Doctype**
    - Use the HTML 5 doctype at the top of your website

    *Bad*
    ```html
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
    "http://w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    ```

    *Good*
    ```html
    <!DOCTYPE html>
    ```

- **HTML5 Markup**
    - Use HTML5 markup syntax

    *Bad*
    ```html
    <div class="header"><!-- old way to do headers --></div>
    ```

    *Good*
    ```html
    <header><!-- my header --></header>
    ```

- **Tables**
    - Tables should NOT be used for layout design. Use CSS.

    *Bad*
    ```html
    <tr class="nav">
        <td>Nav item 1</td>
        <td>Nav item 2</td>
        <td>Nav item 3</td>
    </tr>
    ```

    *Good*
    ```html
    <nav>
        <ul>
            <li>Nav item 1</li>
            <li>Nav item 2</li>
            <li>Nav item 3</li>
        </ul>
    </nav>
    ```

    ```css
    nav li{
        float: left;
        list-style: none;
    }
    ```

- **Naming Conventions**
    - Use object-oriented class names to build scalable and modular markup. Use hyphen syntax sparingly. [You can read more about OOCSS at Smashing Magazine.](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/)

    *Bad*
    ```html
    <div class="homePageProductContainer"></div>

    <button class="checkout-button"></div>
    <button class="signup-button"></div>
    ```

    ```css
    .homePageProductContainer{
        color: tomato;
        padding: 1rem;
    }

    .checkout-button{
        border-radius: 5px;
        color: tomato;
        padding: 1rem;
    }

    .signup-button{
        border-radius: 5px;
        color: magenta;
        padding: 1rem;
    }
    ```

    *Good*
    ```html
    <div class="product-container home"></div>

    <button class="button checkout"></div>
    <button class="button signup"></div>
    ```

    ```css
    .product-container.home{
        color: tomato;
        padding: 1rem;
    }

    .button{
        border-radius: 5px;
        padding: 1rem;
    }

    .button.checkout{
        color: tomato;
    }

    .button.signup{
        color: magenta;
    }
    ```

- **Comments**
    - Limit the use of rendered comments for production (js & css comments get removed/ minified)
    - Don't use "end div" comments. Use the inspector and dev tools to debug html/ css
    - Comments should be implemented with liquid syntax
    - Use liquid comments instead of HTML comments when possible

    *Good*
    ```html
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

- **Minimum DOM Size**
    - Keep the DOM size to a minimum and don't use unnecessary elements

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

    - Avoid using foundation classes to hide/show mobile and desktop versions of similar elements. Instead use CSS to transform these elements so that they look good at any screen size. This is especially important for product displays as they are very heavy for both the server and customer viewing the site.

    *Bad*
    ```html
    <div class="list hide-for-small">
        <!-- desktop advanced list -->
    </div>

    <div class="list show-for-medium-up">
        <!-- mobile advanced list -->
    </div>
    ```

    *Good*
    ```html
    <div class="list">
        <!-- advanced list that looks good at all sizes -->
    </div>
    ```

- **Images**
    - Use the asset_url for including images and other assets
    - `asset_url` returns asset path relative to the current theme’s asset directory on the cdn

    *Bad*
    ```html
    <img src="files/assets/myimage.jpg">
    ```

    *Good*
    ```html
    <img src="{{ "myimage.jpg" | asset_url }}">
    ```

    *Output*
    ```html
    <img src="http://cdn2.crystalcommerce.com/themes/clients/MyClient/assets/myimage.jpg">
    ```

    - Alt values: Static images require an alt value for accessibility and SEO. The alt value should reflect the content of the image (assuming there is no text describing it nearby) and the action if applicable. If the image is purely decorative, use the CSS `background-image` property instead to remove it from the document. [Read more about alt accessibility at webaim.org.](http://webaim.org/techniques/alttext/)

    *Bad*
    ```html
    <a href="/george_washington" class="portrait">
        <img src="{{ "president.jpg" | asset_url }}" alt="">
    </a>

    <img src="{{ "decorative-scroll.jpg" | asset_url }}" alt="">

    <p>Everyone's favorite president</p>
    ```

    *Good*
    ```html
    <a href="/george_washington">
        <img src="{{ "president.jpg" | asset_url }}" alt="A painting of George Washington. Click to learn more about him.">
    </a>
    
    <p>Everyone's favorite president</p>
    ```

    ```css
    .portrait::after{
        background-image: url('assets/img/decorative-scroll.jpg');
        content: '';
    }
    ```

- **Form Fields**
    - Use `<label>` fields to label each form field. The for attribute should associate itself with the input field, so users can click the labels and obtain focus. Using the placeholder value alone is not adequate because it is often skipped by screen-readers. [Read more about accessible web forms at webaim.org](http://webaim.org/techniques/forms/controls)
    
    *Bad*
    ```html
    <input id="name" type="text" placeholder="Enter your name">
    ```

    *Good*
    ```html
    <label for="name">Your Name</label>
    <input id="name" type="text" placeholder="Enter your name">
    ```

- **Liquid Logic**
    - Avoid long liquid statements that have lots of operators. Simplify your statements using available tools such as `{% assign %}`, `{% for %}`, `{% unless %}`, and `{% != %}'`.

    *Bad*
    ```html
    {% if site.pagename == 'home' or site.pagename == 'buylist' or site.pagename == 'about_us' or site.pagename == 'multi_search' or site.pagename == 'category_browse'  or [...] %} 
        <!-- show this thing -->
    {% endif %}
    ```

    *Good*
    ```html
    {% if site.pagename != 'advanced_search' %}
        <!-- show this thing -->
    {% endif %}
    ```

### <a name='css'>CSS</a>

- **Formatting**: 
    - All CSS declarations should have a space after the property colon and a trailing semi-colon. 
    - CSS properties should be alphabetized (use your best judgment if there are prefixes). 
    - Put a hard return after each selector's closing `}`. 
    - Do not nest rules with indentation.

    *Bad*
    ```CSS
    div{
        padding:1em;
        border-radius:5px;
        border: 1px solid tomato;
        -webkit-border-radius: 5px;
        -moz-border-radius: 5px
        }
        div a{
            padding: 1.5em;
        }
    ```
    *Good*
    ```CSS
    div{
        border: 1px solid tomato;
        padding: 1em;

        border-radius: 5px;
        -moz-border-radius: 5px;
        -webkit-border-radius: 5px;
    }

    div a{
        padding: 1.5em;
    }
    ```

- **CSS3 Over Images**
    - Use CSS3 properties whenever possible to avoid the usage of images. Check [can I use](http://caniuse.com/) for newer CSS properties (such as clip-mask) to ensure they are decently supported.

    *Bad*
    ```html
    <a href="/sign_up">
        <img src="{{ "button.jpg" | asset_url }}" alt="Go to sign up page">
    </a>
    ```

    *Good*
    ```html
    <a href="/sign_up" class="button sign-up">Sign Up!</a>
    ```

    ```css
    .button{
        border-radius: 5px;
        border: 1px solid black;
        padding: 1rem;
    }

    .sign-up{
        background: -webkit-gradient(linear, left top, left bottom, 
                    color-stop(0%,rgba(255,255,255,1)), 
                    color-stop(100%,rgba(200,200,200,1)));
                    color: white;
    }
    ```

- **Units**: 
    - 0 value requires no units.

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

    - Use responsive units whenever possible.

    *Bad*
    ```css
    .my-div{
        font-size: 10pt;
        width: 125px;
    }
    ```

    *Good*
    ```css
    .my-div{
        font-size: 1em;
        width: 10%;
    }
    ```

- **IDs and Class names**
    - The use of IDs is not allowed in CSS and should only be used for Javascript.

    *Bad*
    ```css
    #my-div {background: blue;}
    ```

    *Good*
    ```css
    .my-div {background: blue;}
    ```

- **Hacks**
    - Any CSS hacks should be external from the main CSS document, and should be well commented on why you are using the hack

    *Bad*
    ```css
    /* custom.global.css */

    #page-container {background: #000 !important;}
    ```

    *Good*
    ```css
    /* custom.shame.css */

    /*  
    *    Style set with Javascript so I
    *    need to overwrite it with !important   
    */

    #page-container { background: #000 !important;}
    ```

- **Selectors**
    - CSS selectors should not exceed 3 levels deep. If they do, add a class to the element you are selecting. [Read why at csswizardry.com.](http://csswizardry.com/2012/05/keep-your-css-selectors-short/)

    *Bad*
    ```css
    .content .product-container > .product .inner .name + .price {
        font-weight: bold;
    }
    ```

    *Good*
    ```css
    .product-container .price {
        font-weight: bold;
    }
    ```

- **Organization**
    - Do not use multiple selector declarations to write duplicate styles or to style the same element. 

    *Bad*
    ```html
    <h4><p>My content<p></h4>
    ```

    ```css
    h4{
        font-family: 'Helvetica', 'Arial', sans-serif;
    }

    p{
        color: tomato;
        font-family: 'Helvetica', 'Arial', sans-serif;
    }

    [...]

    p{
        font-weight: bold;
    }
    ```

    *Good*
    ```html
    <h4><p>My content<p></h4>
    ```

    ```css
    h4, p{
        font-family: 'Helvetica', 'Arial', sans-serif;
    }

    p{
        color: tomato;
        font-weight: bold;
    }
    ```

    - Sections of CSS should be labeled with a comment head that is prefixed with an underscore.

    *Bad*
    ```css
    header{
        background: tomato;
    }
    ```

    *Good*
    ```css
    /*===== _HEADER ======*/
    /*====================*/

    header{
        background: tomato;
    }
    ```

- **Use shorthand when available**
    - Don't know what properties have available shorthand? [Dustian Diaz has a great article about them.](http://www.dustindiaz.com/css-shorthand/)

    *Bad*
    ```css
    div{
        margin-bottom: 2em;
        margin-left: auto;
        margin-right: auto;
        margin-top: 1em;
    }
    ```

    *Good*
    ```css
    div{
        margin: 1em auto 2em;
    }
    ```

- **Specify font fallbacks**
    
    *Bad*
    ```css
    p{
        font-family: 'Lato';
    }
    ```

    *Good*
    ```css
    p{
        font-family: 'Lato', 'Helvetica', 'Arial', sans-serif;
    }
    ```

- **Positioning**
    - Use absolute and relative position sparingly.

    *Bad*
    ```css
    div{
        position: relative;
        top: 1em;
    }
    ```
    *Good*
    ```css
    div{
        margin-top: 1em;    
    }
    ```
    
- **rem and em**
    - Use `rem` for font-size and `em` for media queries. 
    - `rem` is not supported in older browsers with media queriers. <sup>[Refrence](https://bugs.webkit.org/show_bug.cgi?id=78295)</sup>
    - `rem` = Size relative to the body element font-size
    - `em` = Size relative the parent element font-size

    *Bad*
    ```css
    div{
        position: relative;
        top: 1em;
    }
    ```
    *Good*
    ```css
    div{
        margin-top: 1em;    
    }
    ```
    
    

### <a name='javascript'>Javascript</a> 

- **Semi-colons**

    *Bad*
    ```Javascript
    (function() {
      var name = 'Skywalker'
      return name
    })()
    ```

    *Good*
    ```Javascript
    (function() {
      var name = 'Skywalker';
      return name;
    })();
    ```

    *Even Better*
    ```Javascript
    ;(function() {
      var name = 'Skywalker';
      return name;
    })();
    ```

- **Use single quotes for strings**

    *Bad*
    ```Javascript
    var myString = "no double quotes \"without\" escapes <div class=\"gross\"></div>"
    ```

    *Good*
    ```Javascript
    var myString = 'now we can "freely" use double quotes <div class="yay"></div>'
    ```

- **Use braces for multi-line blocks**

    *Bad*
    ```Javascript
    if (test)
        return false;
    ```

    *Good*
    ```Javascript

    if(test) return false;

    //or

    if(test){
        return false;
    }
    ```

- **Use `var` to declare variables with camelCase formatting**

    *Bad*
    ```Javascript
    MYsupa_coolVAR = 'please no...';
    ```

    *Good*
    ```Javascript
    var superCool = 'thank you...';
    ```

- **Use evaluation shortcuts**

    *Bad*
    ```Javascript
    if (name !== ''){
        // do this
    }
    ```

    *Good*
    ```Javascript
    if (name){
        // do this
    }
    ```

- **Use literal syntax for object and array creation**

    *Bad*
    ```Javascript
    var items = new Array();

    var fruits = new Object();
    ```

    *Good*
    ```Javascript
    var items = [];

    var fruits = {};
    ```

- **Cache jQuery lookups**

    *Bad*
    ```Javascript
    function setSidebar() {
      $('.sidebar').hide();

      // do this

      $('.sidebar').css({
        'background-color': 'pink'
      });
    }
    ```

    *Good*
    ```Javascript
    function setSidebar() {
      var $sidebar = $('.sidebar');
      $sidebar.hide();

      // do this

      $sidebar.css({
        'background-color': 'pink'
      });
    }
    ```

- **Scope jQuery lookups using `.find()`**
    - [See why at jsperf](http://jsperf.com/jquery-find-vs-context-sel)

    *Bad*
    ```Javascript
    $('.active').on('click', function(){
        // do this
    });
    ```

    *Good*
    ```Javascript
    $('#header').find('.active').on('click', function(){
       // do this 
    });
    ```

- **More**
    - Standards for more advanced javascript and jQuery can be found [here](https://github.com/crystalcommerce/FrontendStandards/blob/master/JAVASCRIPT.md) (Work in progress)

### <a name='perf'>Performance</a>

- **Images:**
    - Font-awesome should be used in place of an image whenever possible.
    - Image sprites should be used when CSS3 styles are not appropriate and called only once. [CSSTricks has a great article about using image sprites](http://css-tricks.com/css-sprites/), and [spritepad is a helpful tool for making them.](http://spritepad.wearekiss.com/)
    - Use as few images as possible.
    - PNGs should be optimized to reduce file size. [TinyPNG is a great tool for this.](https://tinypng.com/). They should also only be used when transparency is important. *Almost all slider images should be jpgs*.


- **Google Fonts**
    - You can include multiple Google Web Fonts with one `<link>` tag. This limits the amount of requests to their server to 1. <sup>[Reference](https://developers.google.com/fonts/docs/getting_started#Syntax)</sup>

    *Bad*
    ```html
    <link href='http://fonts.googleapis.com/css?family=Open+Sans' rel='stylesheet' type='text/css'>
    <link href='http://fonts.googleapis.com/css?family=Roboto' rel='stylesheet' type='text/css'>
    ```

    *Good*
    ```html
    <link href='http://fonts.googleapis.com/css?family=Open+Sans|Roboto' rel='stylesheet' type='text/css'>
    ```

- **Config.yml**
    - Use the `config.yml` to include CSS & JS
    - The config.yml will minify concatenate JS & CSS into fewer files.
    - [More info at docs.cc.com](http://docs.crystalcommerce.com/features/theme_config.html)
    
    *Good*
    ```html
    {% comment %} This minifies the CSS by setting it to false {% endcomment %}
    {{ "head" | css_minify_tag: false }}
    ```

### <a name='seo'>SEO & Data</a>

- **Schema Data**
    - Use schema data when applicable. You can test the data with [Google's Structured Data Testing Tool](http://www.google.com/webmasters/tools/richsnippets). More info at [Schema.org](http://schema.org)
  - [Schema Product Data](http://schema.org/Product)
  - [Schema Organization Data](http://schema.org/Organization)

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

- **Use text instead of images**

    *Bad*
    ```html
    <img src="{{ "fancy_looking_store_name.jpg" | asset_url }} alt="CC's Cards and More!">
    ```

    *Good*
    ```html
    <div class="logotype">CC's Cards and More!</div>
    ```

    ```css
    .logotype{
        color: tomato;
        font-weight: 2em;
        font-family: 'Raleway', 'Helvetica', 'Arial', sans-serif;
    }
    ```

### <a name='moreresources'>External Resources</a>

- [View more resources](https://github.com/crystalcommerce/Heisenberg/wiki/External-Resources)
- [TMW Front-end guidelines](https://github.com/tmwagency/TMW-frontend-guidelines/blob/master/Front-End%20development%20guidelines.mdown)
