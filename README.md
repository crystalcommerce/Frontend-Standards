# Coding Standards

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

### <a name='moreresources'>More Resources</a>

**Refrence**
- [HTML5 Doctor](http://html5doctor.com/)


**Tools**
- [Siteleaf Liquid Syntaxt (Sublime Text2 Package)](https://sublime.wbond.net/packages/Siteleaf%20Liquid%20Syntax)

---

---

---


# Example from AirB n B formatting
## <a name='arrays'>Arrays</a>

  - Use the literal syntax for array creation

    ```javascript
    // bad
    var items = new Array();

    // good
    var items = [];
    ```

  - If you don't know array length use Array#push.

    ```javascript
    var someStack = [];


    // bad
    someStack[someStack.length] = 'abracadabra';

    // good
    someStack.push('abracadabra');
    ```
