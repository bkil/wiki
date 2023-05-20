# Opera Mini

See also for guidelines generalized from the below limitations:

* [optimizing-web-proxy-guidelines.md](optimizing-web-proxy-guidelines.md)

Details are listed for Opera Mini 5.0+.

## TODO

Note that this is a draft based on various online posts and articles published over the years.
More first hand experimentation would be needed to validate some of the limitations.

* meta refresh
* postMessage
* XHR ontimeout, onerror
* deadline for fetching the whole page source, maybe this itself is set at 6 seconds
* Can you search for characters outside ISO-8859-1 on a page client side?
* Can you search for text spanning multiple rectangles on a page client side?
* Can an anchor link scroll horizontally (in two dimensions) between targets client side?
* Is the OBML sent to the client compressed?

### Keyboard

The difficulty of typing characters on the on-screen keypad of Opera Mini running on micro emulator by order of screen depth are the following:

* `[a-z./ ]`, backspace, cancel, enter,
* `[0-9()+*=&_'"@?!;:,%#-]`
* `[][$<>{}^\\~|]`

Missing:

```
`
```

## Empirical

* The time to first byte must be less than about 6 seconds, otherwise it will stop with an error message
* no: wasm, AVIF
* yes: WebP

## Metadata

* Text is encoded as UTF-8
* TLS certificate expiry, status, common name and details are forwarded, so watch out for how much data you put in these fields.
* The base URL prefix of the page is omitted from intra-site links
* head metadata for bookmarking: title, favicon, RSS alternate
* The proxy server adds X-Forwarded-For HTTP request header towards the origin
* Cookies: 60/domain, 5117 byte/cookie, 12093 byte/domain

## JavaScript

* ES5
* the page is progressively streamed to the client during the time it is downloaded or manipulated by JavaScript
* paused after at most about 5 seconds from start of page loading until next interaction
* setTimeout(), setInterval(), XMLHttpRequest() supported
* form: onSubmit, onChange
* mouseover, mousedown, mouseup, click events fired at once
* focus and blur only on form input elements
* `console.log()`
* `body.onload()`
* `onclick` handlers on a link may sometimes be ignored after a minute if it also includes an href, substituting the action with top level navigation executed on a different proxy server, thus losing application state

## Unsupported

### Unsupported HTML

* HTML5 form validation
* video, audio
* viewport meta
* blink, marquee

### Unsupported CSS

* border-radius
* linear-gradient (remember to set a background-color fallback!)
* background-attachment, box-shadow, border-image
* web fonts (use SVG `<img>` instead for icons): the default one used is usually sans serif, also includes a tiny font covering ISO-8859-1
* font-family: monospace is simulated by spacing characters from the default font, other values ignored
* CSS and SVG SMIL animations: only first frame shown
* CSS transition, transform
* blur-radius of text-shadow (text-shadow is simulated with overlays)
* dotted and dashed borders rendered as solid
* line-height
* overflow: will always clip (only the body element is scrollable)

### Unsupported JavaScript

* partially supported: unload event
* in `strict mode`, const and let are treated as reserved words
* events never fired: contextmenu, dblclick, error, keydown, keypress, keyup, mousemove, mouseenter, mouseleave, mouseout, mousewheel, resize, scroll, touchcancel, touchend, touchmove, touchstart
* `window.open()` and anchor target triggers loading page in a separate screen instead
* `window.close()`
* localStorage, sessionStorage, Application Cache, Web SQL, IndexedDB
* Web Workers

## Debug

* `server:source`
* `server:console`
* `debug:`

## Formatting on a single page

* Rectangles positioned according to pixel coordinates
* Raster and vector images are decomposed to reusable sprite rectangles, compressed as PNG or JPEG and specify the average color as a placeholder
* Text rectangles
* A single clickable action can be shared between multiple rectangles
* A single device-specific font
* Codepoints outside the default font are transferred as sprites
* Font sizes: small, medium, large, extra large
* Text decoration: bold
* Color filled rectangles, also used for underline, overline, strike and borders
* Color: 32-bit ARGB
* Each rectangle (row) of text and form field has an explicit foreground text color

## Results in a round trip

* handlers: onclick outside forms, form onsubmit, form onchange
* A form containing a single text input field will also be submitted after changing that field
* onsubmit batches and fires all onclick events for form elements
* Link to be downloaded: flows through the proxy (to maintain origin and cookies)
* Viewing a full original image
* Any element styled with `cursor:pointer`

## Does not result in a round trip

* Scrolling
* Zooming
* Choosing between form select options: all options are preloaded
* Switching between radio button choices
* Toggling checkboxes
* Changing input line text
* Changing a multi-line textarea
* Clicking internal anchor links: scrolls upper left to given position
* Native platform links (e.g., `mailto:`)
* External links with a native mime type handler installed (e.g., an RTSP stream may open through the native media player)

## Approximation

```
font-family: sans-serif;
line-height: 1.1;
white-space: pre;
```

## References

* https://dev.opera.com/articles/opera-mini-content-authoring-guidelines/
* https://dev.opera.com/articles/opera-binary-markup-language/
* https://dev.opera.com/articles/opera-mini-and-javascript/
* https://dev.opera.com/blog/opera-mini-server-upgrade/
* https://dev.opera.com/articles/making-sites-work-opera-mini/
* https://dev.opera.com/blog/opera-mini-5-beta-for-android-phones/
* https://dev.opera.com/blog/opera-standards-chart/
* https://raw.githubusercontent.com/operasoftware/devopera-static-backup/869f534aded1bade5d626af152c6aac36b4e8553/http/dev.opera.com/articles/view/javascript-support-in-opera-mini-4/index.html
* https://dev.opera.com/blog/how-media-queries-allow-you-to-optimize-svg-icons-for-several-sizes/
* https://dev.opera.com/articles/installing-opera-mini-on-your-computer/
* https://dev.opera.com/blog/viewing-and-exporting-source-in-opera-mini/
* https://dev.opera.com/articles/opera-mini-request-headers/
* https://raw.githubusercontent.com/operasoftware/devopera-static-backup/869f534aded1bade5d626af152c6aac36b4e8553/http/dev.opera.com/articles/view/opera-mini-5-developers/index.html
* https://github.com/grawity/obml-parser/blob/master/obml.md
* http://ompd-proxy.narod.ru/
* https://en.wikipedia.org/wiki/Opera_mini
* https://en.wikipedia.org/wiki/Presto_(browser_engine)#Web_browsers
