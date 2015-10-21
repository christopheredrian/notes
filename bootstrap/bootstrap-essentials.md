Summary Steps
=================
1. Layout
2. Typography
3. Use Glyphicons on every dry area
4. Standout content
5. Put well on div
6. Amplify buttons
7. Put the navbar
    - Brand icon
    - Navbar brand
8. Put nav
9. Check for mobile
    - Make navigation collapsable
10. Put the nav dropdown with dividers
Pre-requisite
==================

1. On head
`<link href='bootstrap.min.css' rel='stylesheet'>`
2. On body: Add jQuery library
3. After the jQuery library: 

```html
<script src='bootstrap.min.js'>
</script>
```

*   .container -> centers the div with responsive css
*   .container-fluid -> takes up entire page, grows with the page
Usage: when you want the content to stand-out, fill the entire width of the page.


*   .col-xs-*           0px
*   .col-sm-*           tablets 768px
*   .col-md-*			968px
*   .col-offset-sm-*	Adds a padding column to the left
*   .col-offset-sm-0	
COMBINATION
-----------
**row**  
```
-divA c='col-sm-6 col-xs-10 col-xs-offset-1 col-sm-offset-0'  
-divB c='col-sm-6 col-xs-10 col-xs-offset-1 col-sm-offset-0'  
-- on xs device this will be displayed as   
A _ - - - - - - - - - - _  |
B _ - - - - - - - - - - _   
-- on sm  
A- - - - - - |B - - - - - -   
```

*   .hidden-*		example
`<div class='hidden-sm hidden-xs'>`
Hides the element if screen is sm/xs

*   .visible-*		div.visible-md
Inverse of hidden, only shows when display is medium

Typography
===============
**Default font-size of bootstrap is 14px**
*   .lead 
    - to make text stand out 
*   .text-*
    - *= justify/nowrap/right/left/center

Using Glyphicons
-----------------

#### Using glyphicons with text - this will put it above the text

```html
<div class="feature">
    <i class="glyphicon glyphicon-*"></i>
    <h3>Find your perfect guitar now!</h3>
    <p>This will help you...</p>
</div>
```
##### Now on CSS to customize
```css
.feature .glyphicon{
 font-size: 1.5em;      // enlarge
 color: red;            // color
}
```

*   .list-unstyled  - removes style on bullets
*   .list-inline    - lists all links inline

Buttons and Wells
=====================
### Inset Effect

```html
<div class="row well well-lg">
    <div>
        <button type="button btn btn-lg">Hello!</button>
    </div>
</div>
```
*   well - bordered and grayed background
*   well-* **lg/sm** - optional: more/less padding
*   btn - Required default md size button
*   btn-* **(lg/sm/xs)** - button size
*   btn-default - white
*   btn-primary - blue
        - (default, primary, info, danger, success, warning)

Navigation
===================
**Bootstrap doesn't rely on grids, so just use a container class**

```html
<div class="navbar navbar-default navbar-static-top">
    <div class="container">
        <a href="/" class="navbar-brand">CodeBook</a>
        <ul class="nav">
            <li>Home</li>
            <li>Profile</li>
            <li>Account</li>
        </ul>

    </div>
</div>
```
*   .navbar - starting
    - navbar-(default/inverse) - color
*   .navbar-static-(top/bottom/fixed-top/fixed-bottom)
*   .navbar-brand - Puts the element to the far-left of the navigation

*   .nav - starting point
*   .nav-*
    - pills -> links horizontally
    - tabs -> tabbed navigation bar
        - `class="active"` to the `<li>`
    - navbar-nav   -> inline-horizontally, pills without border
*   .navbar-right -> positons to the right

#### .navbar vs .nav

    .nav - you can have more than one of these such as
        - pills
        - tabs
        - selection
    .navbar - only one

Javascript Components
=======================

Navigation in Extra Small Mode
----------------------------------

```html
<div class="navbar navbar-default navbar-static-top">
    <div class="container">
        <div class="navbar-header">
            <a href="/" class="navbar-brand">TODO: CodeBook</a>
            <button class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
            
                <span class="sr-only">TODO: Toggle navigation</span>
                <!--
                    Although this is fine, it won't scale correctly so we use the one below
                 <i class="glyphicon glyphicon-align-justify"></i>
                  --> 

                  <!-- Use three icon-bar instead -->
                  <span class="icon-bar"></span>
                  <span class="icon-bar"></span>
                  <span class="icon-bar"></span>
            </button>
        </div>
        <ul class="nav navbar-nav navbar-right collapse navbar-collapse">
            <li><a href="">TODO: Home</a></li>
            <li><a href="">TODO: Profile</a></li>
            <li><a href="">TODO: Account</a></li>
        </ul>

    </div>
</div>
```

1. Add the **collapse** class on the navbar _this will hide the element in **ALL** resolutions_
    - .collapse.in - shows the content
2. Bootstrap suggest to add the `.navbar-collapse` _this will cause the elements to show on **sm** and above so it will only be hidden on **xs**_
3. Before the nav list add a button
    - `<span class="sr-only">Toggle navigation</span>` _for screen readers_
    - `button class="navbar-toggle"` _this floats the button to the far right_
        - (pull-left/pull-right)
    - Add the desired glyphicon in this case three `icon-bar`
4. Add plugin(Javascript)
    - `data-toggle="collapse"` 
    - `data-target=".navbar-collapse">` _this is the behavior_
    **This will remove the collapse class on the `.navbar-collapse` element**
5. Wrap with `class="navbar-header"` _This will take entire width of navbar on xs screens_ pushing the other elements below


####Add `data-*` attributes to HTML to use __Javascript plugins__

##Accordion - one at a time toggle

`data-toggle='collapse' data-parent=".panel-group"`


Grouping links in navigation bar
===============================

```html
<div class="navbar navbar-default navbar-static-top">
    <div class="container">
        <div class="navbar-header">
            <a href="/" class="navbar-brand">TODO: CodeBook</a>
            <button class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
            
                <span class="sr-only">TODO: Toggle navigation</span>
                <!--
                    Although this is fine, it won't scale correctly so we use the one below
                 <i class="glyphicon glyphicon-align-justify"></i>
                  --> 

                  <!-- Use three icon-bar instead -->
                  <span class="icon-bar"></span>
                  <span class="icon-bar"></span>
                  <span class="icon-bar"></span>
            </button>
        </div>
        <ul class="nav navbar-nav navbar-right collapse navbar-collapse">
            <li><a href="#">TODO: Home</a></li>
            <li><a href="#">TODO: Profile</a></li>
            <li>
                <a href="about.html" data-target="#" data-toggle="dropdown">TODO: Other<span class="caret"></span></a>
                <ul class="dropdown-menu">
                    <li><a href="#">Settings</a></li>
                    <li class="divider"></li>
                    <li><a href="#">Edit Profile</a></li>
                </ul>
            </li>
        </ul>

    </div>
</div>
```

*   .caret
*   .dropdown-menu
*   `data-toggle='dropdown'` _this will add a class of `open` to the parent li_ which will open the dropdown
*   `<li class="divider"></li>`

Gracefully degrade with older browsers
----------------------------------------

`href="about.html" data-target="#"`

Instead of the `href="#"`