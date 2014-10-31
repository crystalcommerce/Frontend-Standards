# Coding Standards

Coding standards to come...

### <a name='types'>HTML & Liquid</a>

- **HTML 5 Doctype**: Use the HTML 5 doctype at the top of your website

`<!DOCTYPE html>`

- **HTML5 Markup**: Use HTML5 markup syntax when needed
- **Comments**
    - Limit the use of comments for production
    - don't use "end div" comments
    - comments should be implemented with liquid syntax

*Good Example*
```
{% comment %}<!-- My Comments Here --> {% endcomment %}
```

*Bad Example*
```
<!-- My Comments Here -->
```




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
