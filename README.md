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


## <a name='types'>Types</a>

  - **Primitives**: When you access a primitive type you work directly on its value

    + `string`
    + `number`
    + `boolean`
    + `null`
    + `undefined`

    ```javascript
    var foo = 1,
        bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```
