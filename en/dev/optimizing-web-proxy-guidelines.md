# Web page authoring guidelines relating to optimizing web proxy support

For external references about concrete implementation, see:

* [opera-mini.md](opera-mini.md)
* other active: UC Mini Browser, Amazon Silk, Puffin
* defunct: MarioNet, Skweezer, Vision Mobile, OnSpeed, Bolt, Chrome Data Saver

## Goal

* Web proxy solutions for improving efficiency of consuming content on mobile devices
* May allow for reduced client hardware complexity
* May target consuming as little data traffic between the proxy and the client device as possible
* Show critical top part of page content with a low latency to the client

### Response time

* Total time for DNS resolution, socket connection, TLS handshake and time to first byte should be within 5 seconds

### Responsive design

* Support a minimal resolution of 240x320
* Test with multiple client font size zoom levels
* Support a minimal color depth of 15 bits per pixel
* Support monochromatic e-ink down to 16 shades of gray
* Support viewing with images disabled: fill in alt text and longdesc attributes and ensure they do not alter layout
* Provide for reducing decoration and animation according to either the URI, a checkbox or a cookie
* Try not to transfer too much text on a single page at once, as a proxy protocol may transfer text uncompressed and rendering and scrolling through a large canvas may also be inefficient

## HTML

### HTML usable

* cookies: max. 20, max. 4093 bytes/domain
* basic auth
* form input field, text area, checkbox, radio button, submit button, placeholder
* head metadata for bookmarking: title, favicon, RSS alternate
* Unicode text encoded as UTF-8
* Internal anchor links for scrolling
* Links with native platform handlers

### HTML overhead

* Vector graphics and canvas are transformed into raster image sprites of PNG or JPEG
* When the client disables showing of images, each sprite placeholder may carry metadata for average color, size and original URL
* Clickable targets (links and click events) leading to too many different destination
* Clickable targets whose shape must be assembled from multiple rectangles
* Too many form select options transferred at once on a single page
* Using too many code points outside ISO-8859-1: need to be transferred via sprites for small text or if the device lacks native support

### HTML to avoid

* HTML5 form validation
* video, audio
* blink, marquee
* expecting to scroll within an iframe
* spell checking
* indeterminate checkbox

## CSS

### CSS usable

Not an overhead for a single stretch (up to a line) of text:

* color
* font-family: sans-serif
* font-weight: normal, bold
* font-size: use at most 3-4 different sizes within a page
* line-height: 1.1
* white-space: pre
* media-queries can be useful to optimize SVG icons to device resolution

### CSS overhead

* drawn with lines: border, text-decoration: underline, overline, strike-through
* monospace font-family requires transferring characters in individual rectangles
* background-color: drawn individually by filled rectangles
* Interactive CSS properties may cause a round trip such as :target, :active, :checked, :empty

### CSS to avoid

* :hover
* border-radius
* linear-gradient
* background-attachment, box-shadow, border-image
* font-style: italic
* web fonts
* SVG SMIL animation
* CSS animation, transition, transform
* blur-radius
* text-shadow
* dotted or dasher borders
* overflow: scroll, auto

## JavaScript

* Maintaining accessibility without JavaScript is the most straightforward solution

### JavaScript usable

* Should finish execution within 5 seconds upon first load and after each interaction
* Syntax: prefer ES5, but recent additions should also work on most proxy servers

May use, but might cost latency, jitter and potential errors on timeout, hence inline the requested JSON within the body or in a referenced script could prove more reliable:

* XMLHttpRequest

### JavaScript overhead

Within the snapshot deadline, the page may be incrementally or repeatedly downloaded to the client when external resources cause unintended reflow or JavaScript animates and scheduling using it may lead to race conditions:

* setTimeout()
* setInterval()

Always specify extents of external resources such as images to avoid reflow.

If you can't avoid to produce content incrementally, prefer to add new content either by overwriting parts rendered in a static fashion or append it to the end of the document to not cause movement of any existing element.

Some proxy protocols may support rendering using relative coordinates between elements, but even this optimization could prove ineffective in handling changes to text wrapping.

### JavaScript to avoid

* window.open()
* window.close()
* localStorage
* sessionStorage
* Application Cache
* Web SQL
* IndexedDB
* Web Workers

### Events usable

* body.onload
* submit
* click

May use, but if possible, don't depend on these:

* change
* unload

### Events to avoid

* hashchange
* contextmenu, dblclick, error, keydown, keypress, keyup, mousemove, mouseenter, mouseleave, mouseout, mousewheel, resize, scroll, touchcancel, touchend, touchmove, touchstart

## References

* https://tests.caniuse.com/
* https://explore.whatismybrowser.com/useragents/parse/331890850-instagram-android-jad-al50-webkit
