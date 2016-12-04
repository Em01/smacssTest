/* General */
Categorisation is the foundation of smacss:
* Base
* Layout
* Module
* State
* Theme

Decoupling of CSS from HTML.

/* Base Rules */
Keep this as simple as possible:
* Regular element selectors
* CSS resets
* Element selectors
* Normalize

body {
  margin: 0;
}
p {
  color: red;
}

/* Layout Rules */
* Think about the main layout containers on the page, for example:
* Sidebar
* Header
* Footer
* Navigation
* Main Content
Major containing elements & Grid system.

Then consider what will go in to these which will lead you to modules.

* Consider what the div is doing that is different from all the other HTML elements that
are on the page. What is the CSS that you have to write to style the div to get it to do what you 
want it to do.

-major (header, footer, sidebar-only appear once within a page)
-minor (forms buttons navigation components-contained elements)

A Layout should specify the Widths & Margins.
Use class over ID
Specificity can be dangerous.

.layout-header {}
 
Alternatively-

.l-container{
  
}

.l-container #main-content{
  
}

.l-vertical-list > li {
  
}

Could have the Grid system in one file and Layout in another
.container_12.grid_4{
  width: 500px
}

/* Module Rules */
* Essentially these are the content pieces e.g:
* Tabs
* Buttons
* Customised list view

A module is what will contain the content & likely are the majority of the site.
A Module should be its own file with a single name e.g .tab, .btn
A Module should have no hypens. 
Variations of a Module are submodules, they are built on top of the bae modules and they
are prefixed with the modules name.
Dont do modal.large or modal.small because the large class names could be used elsewhere and 
will create potential overrides.
Each Module is an interface that users have to learn.
A Module is code that is written, delivered (to the end user) & maintained.
Consider a repeating pattern a module. It is an encapsulated module which goes into
part of the layout.

* Reusable component likely to sit within a layout component
* Always use classnames
* Examples of modules could include: img, arrows, tables, modal, dropdown & Flags.
* Identify base modules and then what are the base variations-what are the submodules?
Module child elements are sub-components-elements that we want to associate with the root module node.


.widget {
  
}

.widget-title {
  
}

Another example is a Modal Dialog:
It always has a header and footer. The content within it could be completely different.
Find a way to identify the HTML element from the body container then associate them with the 
root module.
Decouple styles on the outside container that could affect styles on the inside.

Sub-modules:
When you have something that needs to appear in a slightly different way e.g:
* Buttons-small, large, dark
* A sub-modules must need to include the base Module otherwise it is not a submodule.
* Prefix with the modules name

Consider the inception rule, If there is need to go three levels deep or more consider refactoring.



/* State rules */
Not applied to base elements, Applied to speciic modules.
When you hover on a button how does it change state?
States are likely a module variation but indicate a JavaScript dependency.

* show or hide
* Open or Closed
.tab {
  
}

.is-tab-active {
  
}

An alternative could be:

.tab-is-active{
}

States that are specific to a module should include the module name & also be inside the 
Module rules not the global.

Avoid a state affecting more than one module at a time.

Consider attribute selectors

.btn[data-state=default] 
.attr('data-state', 'disabled');

/* Theme Rules */
Used for on the fly style changes. 
Prefix with theme so you indicate you are changing the state
.red-background is bad
It is a helper or theme that might be applied on an existing module or Layout.

Typography System should be a helper class:
.text-xl
.text-m


Nothing should have a selector

Ideally you shouldn't be recompiling the HTML just to say "theme color should be blue".

Tradeoff-

Consider where you want the burden-on the CSS or the HTML, By using it on the HTML it keeps
the CSS simple.


/* BEM */
module-name

module-name--submodule (hypen indicates it is on the same level)

module-name__subcomponent (underscore represents it is a child element & under)

/* Alternative Naming Conventions */
.moduleName
.moduleName-subModule
.moduleName--subComponent

/* Considerations */
* Each class element should start with the name of that file.
* shame.scss is a good place to store things we are not happy with.
* Utility or helper files.
* Don't use long selectors-e.g as below. Remember it is the latter authorname you are 
trying to style-everything else is extraneous.

#comments .comment .meta .authorname {}


* Avoid repetition.
* When there is a minimal difference ideally simplify, for example if a font size had a 
1 px difference could this become either or.
* child combinator selector can be useful e.g
.content-number > a {}
This limits the depth of applicability to stop affecting things we don't want to.
* Ocasionally lengthy names have a place-consider the tradeoff where a list item would have
the class applied on everything.

* + * owl selector: First element will not pick up any style, Every element after will.
