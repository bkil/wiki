# HTML rich text support by desktop widget toolkits

## FLTK

* Provided by the Fl_Help_View widget
* Supports most HTML 2.0 elements and tables
* GIF, JPEG, and PNG images displayed inline
* Tags: a, b, body, br, center, code, dd, dl, dt, em, font, h1, h2, h3, h4, h5, h6, head, hr, i, img, kbd, li, ol, p, pre, strong, table, th, td, tr, title, tt, u, ul, var

https://www.fltk.org/doc-1.4/classFl__Help__View.html#details

## GTK Pango

* Tags: b, big, i, s, span, sub, sup, small, tt, u
* span tag with mostly custom attributes: font_desc, font_family, font_size, font_style, font_weight, font_variant, font_stretch, font_features, fgcolor, bgcolor, fgalpha, bgalpha, underline, underline_color, overline, overline_color, rise, baseline_shift, font_scale, strikethrough, strikethrough_color fallback, lang, letter_spacing, gravity, gravity_hint, show, insert_hyphens, allow_breaks, line_height, text_transform, segment
* Underscore is parsed as a prefix for the accelerator key

https://docs.gtk.org/Pango/pango_markup.html#pango-markup

## Java Swing

Features:

* Supports HTML 3.2 with some extensions
* Provided by HTMLEditorKit for JEditorPane from the package javax.swing.text.html
* Can be extended by replacing the parser
* Tags: a, address, applet, area, b, base, basefont, big, blockquote, body, br, caption, center, cite, code, dd, dfn, dir, div, dl, dt, em, font, form, frame, frameset, h1, h2, h3, h4, h5, h6, head, hr, html, i, img, input, isindex, kbd, li, link, map, menu, meta, noframes, object, ol, option, p, param, pre, s, samp, script, select, small, span, strike, strong, style, sub, sup, table, td, textarea, th, title, tr, tt, u, ul, var
* CSS: font-family, font-style, font-size, font-weight, font, color, background-color, background-image, background-repeat, background-position, background, text-decoration, vertical-align, text-align, margin-top, margin-right, margin-bottom, margin-left, margin, padding-top, padding-right, padding-bottom, padding-left, padding, border-top-style, border-right-style, border-bottom-style, border-left-style, border-style, border-top-color, border-right-color, border-bottom-color, border-left-color, border-color, list-style-image, list-style-type, list-style-position

Reference:

* https://docs.oracle.com/en/java/javase/19/docs/api/java.desktop/javax/swing/text/html/HTMLEditorKit.html
* https://docs.oracle.com/en/java/javase/19/docs/api/java.desktop/javax/swing/text/html/CSS.html
* https://docs.oracle.com/en/java/javase/19/docs/api/java.desktop/javax/swing/text/html/HTML.Tag.html
* https://docs.oracle.com/en/java/javase/19/docs/api/java.desktop/javax/swing/text/html/HTML.Attribute.html

## Qt GUI

Features:

* Provided by widgets built on QTextDocument (such as QLabel, QTextEdit)
* Supports a subset of HTML 4
* Tags: a, address, b, big, blockquote, body, br, center, cite, code, dd, dfn, div, dl, dt, em, font, h1, h2, h3, h4, h5, h6, head, hr, html, i, img, kbd, meta, li, nobr, ol, p, pre, qt, s, samp, small, span, strong, sub, sup, table, tbody, td, tfoot, th, thead, title, tr, tt, u, ul, var
* CSS: background-color, background-image, color, font-family, font-size, font-style, font-weight, text-decoration, font, text-indent, white-space, margin-top, margin-bottom, margin-left, margin-right, padding-top, padding-bottom, padding-left, padding-right, padding, vertical-align, border-collapse, border-color, border-top-color, border-bottom-color, border-left-color, border-right-color, border-style, border-top-style, border-bottom-style, border-left-style, border-right-style, border-width, border-top-width, border-bottom-width, border-left-width, border-right-width, border-top, border-bottom, border-left, border-right, border-top, border-bottom, border, background, page-break-before, page-break-after, float, text-transform, font-kerning, font-variant, word-spacing, line-height, -qt-block-indent, -qt-list-indent, -qt-list-number-prefix, -qt-list-number-suffix, -qt-paragraph-type, -qt-table-type, -qt-user-state,
* CSS 2.1 selector classes except :first-child, :hover and :visited

References:

* https://doc.qt.io/qt-6/richtext-html-subset.html#supported-tags
* https://doc.qt.io/qt-6/qtextedit.html#markdown-prop

## wxWidgets

* Provided by wxHtmlWindow from the wxHTML library
* Can be extended to handle any tag
* Tags: a, address, area, b, big, blockquote, body, br, center, cite, code, dd, div, dl, dt, em, font, hr, h1, h2, h3, h4, h5, h6, i, img, kbd, li, map, meta, ol, p, pre, samp, small, span, strike, strong, sub, sup, table, td, th, title, tr, tt, u, ul
* General CSS: text-align, width, vertical-align, background
* span CSS: color, font-family, font-size, font-style (oblique, italic, normal), font-weight (bold, normal), text-decoration (underline)

https://docs.wxwidgets.org/stable/overview_html.html#overview_html_supptags_list
