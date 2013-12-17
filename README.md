# Coding Standards

HTML Standards 

General:
use the HTML5 doctype
use HTML5 markup syntax when needed
limit the use of comments for production
don’t use “end div” comments
comments should be implemented with liquid syntax
keep DOM tree size to a minimum
the use of ID’s should only be for javascript
use the liquid syntax for including images
<img src=“{{ my-img.jpg | assets_url }}” alt={{ store.name }}>
all javascript and css should be included via config.yml

Naming Conventions:
use object oriented naming conventions
hyphenated naming style, i.e. “<div class="my-div”>"
use general-specific names, examples:
header-main
btn-twitter
sidebar-primary
products should be referred to as products, not “item”

Presentation Considerations:
tabs should be set to 4 spaces
indent appropriately to illustrate nesting
nested elements aren’t allowed in single lines, example:
<div class=“wrap”><i class=“icon”></i></div>
use line breaks liberally, refer to code sample below


Sample: HTML Standards Sample




CSS Standards 

Files located in the "css/crystal” folder should not be edited, so that we are able to push updates without ruining any custom styles.

General:
the developers name and crystal commerce should be noted at top of stylesheet
use custom.css to write all of your styles
use devices-custom.css for your responsive styles
use normalize.css if reset is not present
any css hacks should be written in shame.css
shame.css should be well commented to explain the hack
specificity should not exceed 3 levels deep, example:
.container .child .sub-child {…}
use sparingly, only when necessary
CSS3 should be used over images, when applicable
the use of IDs is not allowed in stylesheets 

Presentation Considerations:
do not nest styles with indentation
group browser prefixes, separate with line breaks
w3c css3 spec should be listed last
css properties should be alphabetized 
sections of css should labeled with a comment head
comment heads should be prefixed with an underscore i.e:
“_Header Main Styles”
include table of contents (list of comment heads)
see example...

Images:
image sprites should be used when CSS3 styles are not appropriate
use as few images as possible
image sprites should be called only once
this should be near the top of your stylesheet
you can use a .sprite class to make this easier
use sprites for hover effects at all costs
