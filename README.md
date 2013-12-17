Coding Standards

### HTML
HTML & Liquid Standards 

General:
* use the HTML5 doctype
* use HTML5 markup syntax when needed
* limit the use of comments for production
* don’t use “end div” comments
* comments should be implemented with liquid syntax
* keep DOM tree size to a minimum
* the use of ID’s should only be for javascript
* use the liquid syntax for including images
``` html
<img src=“{{ my-img.jpg | assets_url }}” alt={{ store.name }}>
```
* all javascript and css should be included via config.yml
