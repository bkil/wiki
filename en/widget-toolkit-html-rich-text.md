# HTML rich text support by desktop widget toolkits

## Android text.Html

* Provided by android.text.Html.fromHtml to be used within a TextView
* Tags: br, p, ul, li, div, span, strong, b, em, cite, dfn, i, big, small, font (color, face=monospace|bold|italic), blockquote, tt, a (href), u, strike, sup, sub, h1, h2, h3, h4, h5, h6, img (src)
* style attributes on block elements (p, ul, li, div, blockquote, h1, h2, h3, h4, h5, h6): text-align (start, center, end)
* style attributes (p, span, li): color, background, background-color, text-decoration (line-through)
* Can be easily extended through the tag handler interface

References:

* https://github.com/aosp-mirror/platform_frameworks_base/blob/db93b81cf5536c272cb47fcc03c4a4ef79006473/core/java/android/text/Html.java#L784
* https://developer.android.com/reference/android/text/Html.html#fromHtml%28java.lang.String%29
* https://developer.android.com/reference/android/widget/TextView#setText(java.lang.CharSequence)

## EFL Evas Textblock

* The advanced syntax is HTML-like, but most tags are not directly compatible
* font (fontconfig), font_weight (normal, thin, ultralight, light, book, medium, semibold, bold, ultrabold, black, extrablack), font_style (normal, oblique, italic), font_width (normal, ultracondensed, extracondensed, condensed, semicondensed, semiexpanded, expanded, extraexpanded, ultraexpanded), lang, font_fallbacks, font_size, font_source, color, underline_color, underline2_color, outline_color, shadow_color, glow_color, glow2_color, strikethrough_color, align (auto, left, right, center, middle), valign (top, bottom, middle, center, baseline, base, %), wrap (word, char, mixed, none), left_margin (reset, px), right_margin (reset, px), underline (on, off, single, double), strikethrough (on, off), backing_color, backing (on, off), style (off, none, plain, shadow, outline, soft_outline, outline_shadow, outline_soft_shadow, glow, far_shadow, soft_shadow or far_soft_shadow, bottom_right, bottom, bottom_left, left, top_left, top, top_right, right), tabstops (px), linesize (px), linerelsize (%), linegap (px), linerelgap (%), item (size, abssize, relsize, vsize, full, ascent), linefill (%), ellipsis, password (on, off)

References:

* https://www.enlightenment.org/develop/legacy/program_guide/evas/textblock_objects
* https://docs.enlightenment.org/auto/evas_textblock_style_page.html
* https://docs.enlightenment.org/stable/elementary/group__Elm__Label.html#details
* https://github.com/Enlightenment/efl/blob/0c0d2c33bcfb71f748eaf7620da9006c6409d72d/src/lib/efl/interfaces/efl_text_style.eo
* https://github.com/Enlightenment/efl/blob/0c0d2c33bcfb71f748eaf7620da9006c6409d72d/src/lib/evas/canvas/efl_canvas_textblock.eo

## FLTK

* Provided by the Fl_Help_View widget
* Supports most HTML 2.0 elements and tables
* GIF, JPEG, and PNG images displayed inline
* Tags: a, b, body, br, center, code, dd, dl, dt, em, font, h1, h2, h3, h4, h5, h6, head, hr, i, img, kbd, li, ol, p, pre, strong, table, th, td, tr, title, tt, u, ul, var

https://www.fltk.org/doc-1.4/classFl__Help__View.html#details

## Fyne.io

* Uses the goldmark CommonMark ("Markdown") parser instead of HTML
* Corresponding HTML tags: ul, ol, li, h1, h2, h3, hr, a, p, code, pre, em, strong, blockquote, img

References:

* https://github.com/fyne-io/fyne/blob/5496b3562f8087e72db368c6231f14caa0fdb26a/widget/markdown.go#L40
* https://fyne.io/blog/2021/09/21/v2.1.html
* https://developer.fyne.io/api/v2.3/widget/richtext.html

## GTK Pango

* Tags: b, big, i, s, span, sub, sup, small, tt, u
* span tag with mostly custom attributes: font_desc, font_family, font_size, font_style, font_weight, font_variant, font_stretch, font_features, fgcolor, bgcolor, fgalpha, bgalpha, underline, underline_color, overline, overline_color, rise, baseline_shift, font_scale, strikethrough, strikethrough_color fallback, lang, letter_spacing, gravity, gravity_hint, show, insert_hyphens, allow_breaks, line_height, text_transform, segment
* Underscore is parsed as a prefix for the accelerator key

https://docs.gtk.org/Pango/pango_markup.html#pango-markup

## Java Swing

Features:

* Supports HTML 3.2 with some extensions
* Provided by HTMLEditorKit for JEditorPane from the package javax.swing.text.html
* Can be extended by replacing the parser object argument
* Tags: a, address, applet, area, b, base, basefont, big, blockquote, body, br, caption, center, cite, code, dd, dfn, dir, div, dl, dt, em, font, form, frame, frameset, h1, h2, h3, h4, h5, h6, head, hr, html, i, img, input, isindex, kbd, li, link, map, menu, meta, noframes, object, ol, option, p, param, pre, s, samp, script, select, small, span, strike, strong, style, sub, sup, table, td, textarea, th, title, tr, tt, u, ul, var
* CSS: font-family, font-style, font-size, font-weight, font, color, background-color, background-image, background-repeat, background-position, background, text-decoration, vertical-align, text-align, margin-top, margin-right, margin-bottom, margin-left, margin, padding-top, padding-right, padding-bottom, padding-left, padding, border-top-style, border-right-style, border-bottom-style, border-left-style, border-style, border-top-color, border-right-color, border-bottom-color, border-left-color, border-color, list-style-image, list-style-type, list-style-position

Reference:

* https://docs.oracle.com/en/java/javase/19/docs/api/java.desktop/javax/swing/text/html/HTMLEditorKit.html
* https://docs.oracle.com/en/java/javase/19/docs/api/java.desktop/javax/swing/text/html/CSS.html
* https://docs.oracle.com/en/java/javase/19/docs/api/java.desktop/javax/swing/text/html/HTML.Tag.html
* https://docs.oracle.com/en/java/javase/19/docs/api/java.desktop/javax/swing/text/html/HTML.Attribute.html

## Java SWT Nebula RichTextViewer

* tags: b, strong, em, u, s, p, span, br, ul, ol, li
* attributes: margin-left, text-align=right, style
* style: background-color, color, font-family, font-size

References:

* https://www.eclipse.org/nebula/releases/latest/javadoc/org/eclipse/nebula/widgets/richtext/RichTextPainter.html#field.summary
* https://www.eclipse.org/nebula/releases/latest/javadoc/constant-values.html#org.eclipse.nebula.widgets.richtext.RichTextPainter.ATTRIBUTE_PARAGRAPH_MARGIN_LEFT
* https://www.eclipse.org/nebula/widgets/richtext/richtext.php
* https://github.com/eclipse/nebula/tree/master/widgets/richtext

## Kivy

* Uses the docutils reStructuredText parser instead of HTML
* Corresponding HTML tags: title, b, i, code, p, blockquote, pre, ul, ol, li, img, dl, dt, dd, table, th, tr, td, video
* Custom: SystemMessage, Warning, FieldList, FieldName, FieldBody, Note, Footnote, Entry, Transition
* Roles: :abbreviation:, :acronym:, :code:, :emphasis:, :literal:, :math:, :pep-reference:, :rfc-reference:, :strong:, :subscript:, :superscript:, :title-reference:

References:

* https://github.com/kivy/kivy/blob/39c1f74a68b2e709dcfbdb1a581db05d9fafaf29/kivy/uix/rst.py#L127
* https://docutils.sourceforge.io/rst.html

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

## Unity3D

* Some HTML tags and a few custom ones.
* HTML tags: a, b, br, font, i, nobr, s, sub, sup, u
* custom tags: align, allcaps, alpha, color, cspace, font-weight, gradient, indent, line-height, line-indent, lowercase, margin, mark, mspace, noparse, pos, rotate, size, smallcaps, space, sprite, strikethrough, style, uppercase, voffset, width
* `<style>` is a shorthand for a combination tags

References:

* https://docs.unity3d.com/Manual/UIE-supported-tags.html
* https://docs.unity3d.com/Manual/UIE-rich-text-tags.html
* https://docs.unity3d.com/Manual/UIE-style-sheet.html

## wxWidgets

* Provided by wxHtmlWindow from the wxHTML library
* Can be extended to handle any tag
* Tags: a, address, area, b, big, blockquote, body, br, center, cite, code, dd, div, dl, dt, em, font, hr, h1, h2, h3, h4, h5, h6, i, img, kbd, li, map, meta, ol, p, pre, samp, small, span, strike, strong, sub, sup, table, td, th, title, tr, tt, u, ul
* General CSS: text-align, width, vertical-align, background
* span CSS: color, font-family, font-size, font-style (oblique, italic, normal), font-weight (bold, normal), text-decoration (underline)

https://docs.wxwidgets.org/stable/overview_html.html#overview_html_supptags_list

## Non-HTML

## TODO

## Without any support

### Apple Cocoa NSTextView

* https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/TextUILayer/Concepts/UILayer.html
* https://developer.apple.com/documentation/appkit/nstextview

### CEGUI

### FOX

* http://www.fox-toolkit.org/xml.html
* http://fox-toolkit.org/ref/hierarchy.html
* http://www.fox-toolkit.org/fonts.html

### GNUStep NSTextView

* http://wwwmain.gnustep.org/resources/OpenStepSpec/ApplicationKit/Classes/NSCStringText.html#:~:text=Plain%20and%20Rich

### Java SWT StyledText

You have to specify the textual content and the styling to apply to each byte offset range separately!

* foreground color, background color, font style (normal, bold, italic)
* line background color (i.e., up to the full width of the widget)

References:

* https://www.eclipse.org/articles/StyledText%201/article1.html

## Only through web browser
