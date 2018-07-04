# Branding PaperTrail 


## Images

-   Images are placed in the System/images node.
-   Images must end in .png (if they are a .jpeg or .gif they can be
    safely renamed).
-   Images should be the correct size, if the image is bigger or smaller
    it should be manually resized before importing into System/images.
-   To prevent the images from being overwritten after upgrades, they
    should be permanently checked out.


login\_background.png (320x365) 
--------------------------------

The honeycomb that sits behind the login and password boxes.

papertrail.png (110x26)
-----------------------

The logo that sits in the top left of the main application screen.  
The background should be transparent.

logo.png (320x50)
-----------------

The logo that sits above the honeycomb.  
Add white space to the left of image to center it above the honeycomb.

egis.png (75x25) 
----------------

The egis logo on the bottom right of the screen.

## Email Signatures

Copy the HTML signature contents into `System\templates\template.html`.

Images should be attached to the document and referenced using:  `cid:@{image001.jpg}` where **image001.jpg** is the attachment name. e.g.:

```html
<img border="0" width="141" height="72" src="cid:@{image001.jpg}">
```

The users details can be prepopulated into the template using [standard expressions](/reference/standard-expression-text.md), the following fields will be available:

- name
- email
- tel
- fax
- mobile
- login
- title
- division


>  WARNING: always keep the html in a checked out position to prevent it from being overwritten during upgrades

