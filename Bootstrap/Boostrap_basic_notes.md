# Bootstrap Basics
## What is Bootstrap?
* Bootstrap is a free front-end framework for faster and easier web development.
* Bootstrap includes HTML and CSS based **design templates for typography, forms, buttons, tables, navigation, modals, image carousels and any other** , as well as optional JavaScript plugins.
* Bootstrap also gives you the ability to easily **create responsive designs.**

### What is  Responsive Web Design?
* Responsive web design is about creating web sites which automatically adjust themselves to look good on all devices, from small phones to large desktops.

#
## Notes
* Containers
    * There are two container classes to choose from:
        * The `.container` class provides a responsive fixed width container
        * The `.container-fluid` class provides a full width container, spanning the entire width of the viewport.
* Bootstrap Grid System
    * Bootstrap's grid system allows up to **12 columns** across the page.If you do not want to use all 12 columns individually, you can group the columns together to create wider columns.
    * Bootstrap's **grid system is responsive**, and the columns will re-arrange automatically depending on the screen size.
   
    * **Grid Classes**
        * The Bootstrap grid system has four classes:
            * **xs** (**for phones** - screens less than 768px wide)
            * **sm** (**for tablets** - screens equal to or greater than 768px wide)
            * **md** (**for small laptops** - screens equal to or greater than 992px wide) 
            * **lg** (**for laptops and desktops** - screens equal to or greater than 1200px wide)
    * Ex:
        ```bootstrap
            <div class="row">
                <div class="col-sm-4">.col-sm-4</div>
                <div class="col-sm-4">.col-sm-4</div>
                <div class="col-sm-4">.col-sm-4</div>
            </div>
        ```

* Image Shapes
    * Rounded Corners
        * The .img-rounded class adds rounded corners to an image (IE8 does not support rounded corners):
        * Ex: <img src="cinqueterre.jpg" class="img-rounded" alt="Cinque Terre">
    * Circle
        * The .img-circle class shapes the image to a circle (IE8 does not support rounded corners):
        * <img src="cinqueterre.jpg" class="img-circle" alt="Cinque Terre">
    * Thumbnail
        * The .img-thumbnail class shapes the image to a thumbnail:
        * <img src="cinqueterre.jpg" class="img-thumbnail" alt="Cinque Terre">
    * Response Images
    
    * Responsive Embeds 
        * Also let videos or slideshows scale properly on any device.
        * Classes can be applied directly to <iframe>, <embed>, <video>, and <object> elements.
        * The following example creates a responsive video by adding an .embed-responsive-item class to an <iframe> tag (the video will  then scale nicely to the parent element). The containing <div> defines the aspect ratio of the video:
        Ex: <div class="embed-responsive embed-responsive-16by9">
                <iframe class="embed-responsive-item" src="..."></iframe>
            </div>
    
* Creating a Jumbotron
    * A jumbotron indicates a big box for calling extra attention to some special content or information.
    * A jumbotron is displayed as a grey box with rounded corners. It also enlarges the font sizes of the text inside it.
    * **Tip:** Inside a jumbotron you can put nearly any valid HTML, including other Bootstrap elements/classes.
    * Use a <div> element with class .jumbotron to create a jumbotro.

* Glyphicons
    * Bootstrap provides 260 glyphicons from the Glyphicons Halflings set.
    * Glyphicons can be used in text, buttons, toolbars, navigation, forms, etc.
    * Ex: Envelope glyphicon.

* Badges
    * Badges are numerical indicators of how many items are associated with a link:
    * The numbers (5, 10, and 2) are the badges.
    * Use the `.badge` class within <span> elements to create badges:

* Media Objects
    * Bootstrap provides an easy way to align media objects (like images or videos) to the left or to the right of some content. This can be used to display blog comments, tweets and so on:

* The Carousel Plugin
    * The Carousel plugin is a component for cycling through elements, like a carousel (**slideshow**).
    * **Tip:** Plugins can be included individually (using Bootstrap's individual "carousel.js" file), or all at once (using "bootstrap.js" or "bootstrap.min.js").

* The Modal Plugin
    * The Modal plugin is a dialog box/popup window that is displayed on top of the current page:
    * **TIP:**Plugins can be included individually (using Bootstrap's individual "modal.js" file), or all at once (using "bootstrap.js" or "bootstrap.min.js").