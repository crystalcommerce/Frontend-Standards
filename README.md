# Coding Standards & Guidelines

## Table of Contents

  1. [HTML & Liquid](#html)
  1. [CSS](#css)
  1. [Javascript](#arrays)
  1. [Refrences](#refrences)
  1. [More Resources](#moreresources)

### <a name='html'>HTML & Liquid</a>

- **HTML 5 Doctype**: Use the HTML 5 doctype at the top of your website

    `<!DOCTYPE html>`

- **HTML5 Markup**: Use HTML5 markup syntax

    *Good*
    ```html
    <header><!-- my header --></header>
    ```

    *Bad*
    ```html
    <div class="header"><!-- old way to do headers --></div>
    ```

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
    - `asset_rul` returns asset path relative to the current theme’s asset dir on the cdn

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
    
    


### <a name='css'>CSS</a>

*Work in progress*

General:
- the developers name and crystal commerce should be noted at top of stylesheet
- use custom.css to write all of your styles
- use devices-custom.css for your responsive styles
- use normalize.css if reset is not present
- any css hacks should be written in shame.css
- shame.css should be well commented to explain the hack
- specificity should not exceed 3 levels deep, example:
- .container .child .sub-child {…}
- use sparingly, only when necessary
- CSS3 should be used over images, when applicable
- the use of IDs is not allowed in stylesheets 

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


### <a name='refrences'>Refrences</a>

*Note: Lets keep a list of refrences for the above parts down here*


### <a name='moreresources'>External Resources</a>

- [View more resources](https://github.com/crystalcommerce/Heisenberg/wiki/External-Resources)
