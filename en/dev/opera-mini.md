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

* The content of a bookmark is stored client side and transferred every time it is clicked on
* The time to first byte over the network must be less than about 6 seconds, otherwise it will stop with an error message
* If it detects rapid looping (<150ms) via setTimeout, it starts to compress the interval after 1s by invoking every second one without delay
* A busy loop or a setInterval smaller than 100ms is executed without interruption and sometimes without sending any updates. The page is killed with a transcoder connection timeout after 42s wall clock.
* While the busy loop is running after load, the normal timeout is not initialized. After the first occasion of slack, the timeout is initialized that will pause after 5s of wall time from that point on in the earliest convenience when a busy loop is not running.
* Incremental update is adaptive and may not trigger unless the DOM is changed and the interval is long enough
* An update is reliably sent when the document has stayed unchanged for at least 1.1s or otherwise about once every 1.5-2s depending on cycle time and finally following the normal timeout of ~5.5s
* no: wasm, AVIF
* yes: WebP
* img onerror
* 20 pages can be saved for offline use, but sometimes history and bookmark links can also come from the cache
* Textarea default values are included at the beginning of the stream, followed by interaction rectangles, box lines, text labels and finally images
* Consecutive lines of text of the same style and color can fit a single string block
* In some rare, special circumstances, a preformatted block might get automatically combined into a single string block (mapped to a textarea) if the character spacing is right, but this needs more research. It is otherwise usually layed out one character at a time.
* If loading takes more than 1-2s due to bad radio connection or network load on the proxy, the client will keep retrying the request and the previous, duplicate response may also arrive later. This will bloat the sent or received traffic volume or both.
* the OBML is sent to the client compressed, probably with gzip
* A readonly textarea renders similarly to a pre with overflow hidden
* Supports both PNG and JPEG compression. Seems to select based on number of colors in the original. May results in blurred line diagrams of sometimes larger file size. Images are always recompressed. Low and medium quality: the image is resized to fit the viewport with slight adjustments to quality. High quality: the original image size is preserved, but it is transferred in slices that match the screen size.
* It is much more efficient to define an onclick function handler using the DOM in JavaScript than with HTML or a stringified handler. Also, the act of attaching an onclick handler itself to certain elements may sometimes break up the markup of the displayed layer despite how it is designed and documented.
* Decoration for form widgets is sent as images unless the borders and background are overridden
* Opera mini 4 does not implement incremental rendering, nor transmitting only what changed on screen.
* Top level navigation always takes a few kB more traffic and further latency than when interacting with a single page.
* base-url is not deduced for encoding of anchor references with the same prefix
* Navigation among a table of anchor links is always linear, while onclick of cells and certain submit buttons can be navigated via a 2D pointer.
* The center of the image form submit button is sent as click coordinates
* A textarea can utilize variable width font on some platforms (i.e., where a single font is available)
* The remote application proxy for a page does not keep JavaScript session state for more than 10 minutes if no interaction happens before the deadline. Form submission to a URL and clicking on a link which has a href URL still works correctly.

See test cases:

* https://bkil.gitlab.io/static-wonders.css/mini-board/

## Metadata

* Text is encoded as UTF-8
* TLS certificate expiry, status, common name and details are forwarded, so watch out for how much data you put in these fields.
* The base URL prefix of the page is omitted from intra-site links
* head metadata for bookmarking: title, favicon, RSS alternate
* The proxy server adds X-Forwarded-For HTTP request header towards the origin
* `Accept-Language` HTTP request header is sent
* Cookies: 60/domain, 5117 byte/cookie, 12093 byte/domain
* viewport meta: device-width and initial-scale improve rendering with mobile mode disabled

## CSS

* @supports

## JavaScript

* ES5
* `alert`, `confirm`
* `screen.width`, `screen.availWidth`, `screen.colorDepth` (4), `screen.pixelDepth` (4)
* the page is progressively streamed to the client during the time it is downloaded or manipulated by JavaScript
* paused after at most about 5 seconds from start of page loading until next interaction
* setTimeout(), setInterval(), XMLHttpRequest() supported
* form: onSubmit, onChange
* mouseover, mousedown, mouseup, click events fired at once
* focus and blur only on form input elements
* `console.log()`
* `body.onload()`
* `onclick` handlers on a link may sometimes be ignored after a minute if it also includes an href, substituting the action with top level navigation executed on a different proxy server, thus losing application state
* language locale can be extracted from `navigator.userAgent` or `navigator.appVersion`

## Unsupported

### Unsupported HTML

* HTML5 form validation
* `for` attribute of `label` within forms does not activate radio buttons - could be worked around via onclick or a `select` widget
* video, audio
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
* `navigator.languages` is undefined, `navigator.language`, `navigator.userLanguage`, `navigator.browserLanguage` are always `en`
* `screen.height` and `screen.availHeight` seem to match width

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

* Finding text on the page
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
* https://dev.opera.com/blog/opera-12-10-is-out/
* https://raw.githubusercontent.com/operasoftware/devopera-static-backup/869f534aded1bade5d626af152c6aac36b4e8553/http/dev.opera.com/articles/view/javascript-support-in-opera-mini-4/index.html
* https://github.com/operasoftware/devopera-static-backup/blob/869f534aded1bade5d626af152c6aac36b4e8553/http/dev.opera.com/articles/view/making-small-devices-look-great/index.html
* https://github.com/operasoftware/devopera-static-backup/blob/869f534aded1bade5d626af152c6aac36b4e8553/http/dev.opera.com/articles/view/designing-with-opera-mini-in-mind/index.html
* https://dev.opera.com/blog/how-media-queries-allow-you-to-optimize-svg-icons-for-several-sizes/
* https://dev.opera.com/articles/installing-opera-mini-on-your-computer/
* https://dev.opera.com/blog/viewing-and-exporting-source-in-opera-mini/
* https://dev.opera.com/articles/opera-mini-request-headers/
* https://raw.githubusercontent.com/operasoftware/devopera-static-backup/869f534aded1bade5d626af152c6aac36b4e8553/http/dev.opera.com/articles/view/opera-mini-5-developers/index.html
* https://github.com/grawity/obml-parser/blob/master/obml.md
* http://ompd-proxy.narod.ru/
* https://en.wikipedia.org/wiki/Opera_mini#JavaScript_support
* https://en.wikipedia.org/wiki/Presto_(browser_engine)#Web_browsers
* https://get.opera.com/ftp/pub/opera/linux/1216/
