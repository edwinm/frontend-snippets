# Frontend snippets
Miscellaneous code snippets for web developers because you can't memorize everything.

## Webpage

Basic HTML to start a website

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="description" content="Description of around 200 letters">
    <link rel="stylesheet" href="style.css">
    <script async src='script.js'></script>
</head>
<body>


</body>
</html>
```

If your site is not English, don't forget to change the `lang` attribute.

## HTML section elements

Make your HTML more semantic by using the right elements.

element | description
--- | ---
main | Main content of the page, without header and footer etcetera
article | Part of the page that could stand alone
section | Group related elements together
header | Title, subtitle, author, publication date
footer | Copyright, privacy statement, contact data
nav | Page and site navigation with links
aside | Content that's supplementary to the main content

You can add an `aria-label` attribute to describe the section.

## Autofill

Use the `autocomplete` attribute in your forms so that users can easily fill them out.
Use one of the following values for the `autocomplete` attribute to enable the user the auto fill them.

<details>
<summary>See list of autocomplete attribute values</summary>
<pre>
name
honorific-prefix
given-name
additional-name
family-name
honorific-suffix
nickname
organization-title
username
new-password
current-password
one-time-code
organization
street-address
address-line1
address-line2
address-line3
address-level4
address-level3
address-level2
address-level1
country
country-name
postal-code
cc-name
cc-given-name
cc-additional-name
cc-family-name
cc-number
cc-exp
cc-exp-month
cc-exp-year
cc-csc
cc-type
transaction-currency
transaction-amount
language
bday
bday-day
bday-month
bday-year
sex
url
photo
tel
tel-country-code
tel-national
tel-area-code
tel-local
tel-local-prefix
tel-local-suffix
tel-extension
email
impp
</pre>
</details>


For addresses, you can also add `shipping` and `billing` and for phone numbers, you can add `home`, `work`, `mobile`, `fax` or `pager`.

```html
<input name="shipping-pc" autocomplete="shipping postal-code">
```

Using `new-password` and `current-password` is especially important to make a site work nicely with password managers.

When using `new-password`, you can use the non standard `passwordrules` attribute to specify the rules for a valid password.
See Apple's [Password Rules Validation Tool](https://developer.apple.com/password-rules/).

See the [autofill attribute specification](https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#autofill)
for all possibilities.

## Box sizing

Box sizing border box is easier to work with.

```css
html {
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}
```

## Hyphenation

Turn on hyphenation for the right elements only.

```css
body {
  -webkit-hyphens: auto;
  hyphens: auto;
}

code, var, kbd, samp, tt, dir,
abbr, acronym, blockquote, q {
  -webkit-hyphens: none;
  hyphens: none;
}
```

## Favicon

You can put a favicon.ico in the root of your site and call it a day.

Make sure favicon.ico contains both a 16×16 and 32×32 icon.

If you want to provide an SVG, you can use the code below.

```html
<link rel="icon" href="/favicon.ico" sizes="48x48" >
<link rel="icon" href="/favicon.svg" sizes="any" type="image/svg+xml">
```

See [Definitive edition of "How to Favicon" in 2023](https://dev.to/masakudamatsu/favicon-nightmare-how-to-maintain-sanity-3al7)
by Masa Kudamatsu for more in depth information.

## Social media sharing

Show an image and description when sharing on social media (Facebook, Twitter, LinkedIn, etcetera).

```html
  <meta name="description"
        content="Description of max 200 characters">
  <meta property="og:image" content="https://url-to-image">
  <meta property="og:image:width" content="476">
  <meta property="og:image:height" content="249">
  <meta property="og:image:alt" content="Description of image">
```

By default the page title will be taken from the title element, which often looks like "Page Title - Site Name".
With meta tags, the page title and site name can be defined separately:

```html
  <meta property="og:title" content="Page Title">
  <meta property="og:site_name" content="Site Name">
```

See the [Open Graph protocol](https://ogp.me/) for all possible metadata.

## Progressive Web App

Make your website behave like an app.
With the code below, a user can add the website to their desktop or home screen
and open it as an app without the browser chrome (so, no address bar etcetera).

In your root directory, you need these two files:

`apple-touch-icon.png` - The app icon with a minimal size of 192×192px

`manifest.json` - Contains metadata of the app, see below

This is example content of the `manifest.json` file:

```json
{
    "short_name": "App name",
    "name": "Full name of the app",
    "start_url": "https://example.com/",
    "description": "Description of the app: what does it do?",
    "icons": [
        {
            "src": "/apple-touch-icon.png",
            "sizes": "192x192",
            "type": "image/png"
        }
    ],
    "display": "standalone",
    "background_color": "#ffcccc",
    "theme_color": "#ccccff",
    "categories": ["weblog"]
}
```

See [MDN: Web app manifests](https://developer.mozilla.org/en-US/docs/Web/Manifest) for more options.

Now refer to these files from your HTML:

```html
<link rel="manifest" href="/manifest.json"/>
<link rel="apple-touch-icon" href="/apple-touch-icon.png"/>
<meta name="theme-color" content="#ccccff">
```

You can make your site more app like by adding offline capabilities.
See [Make your PWA feel more like an app](https://web.dev/articles/app-like-pwas) for more ideas.

## CSS animation

Simple CSS animation using transform and transition.

```css
.block {
  transform: translateX(0);
  transition: all 250ms ease;
}

.block.moved {
  transform: translateX(200px);
}
```

For good performance, only animate `transform` and `opacity`.
If performance is still not good, take a look at
the [`will-change`](https://developer.mozilla.org/en-US/docs/Web/CSS/will-change) property.

## Animate to auto height

In CSS, you can't just animate any element to auto height.
By using a grid row, you can.

```css
.container {
  display: grid;
  grid-template-rows: 0fr;
  transition: grid-template-rows 250ms;
}

.container > .inner {
  overflow: hidden;
}

.container:hover {
  grid-template-rows: 1fr;
}
```

## Prefers reduced motion / prefers contrast

Improve the accessibility of your website by reducing animations when requested:

```css
@media (prefers-reduced-motion) {
  * {
    transition-property: none;
  }
}
```

Or increase contrast:

```css
html {
    color: #ccc;
    background-color: white;
}
@media (prefers-contrast: more) {
    html {
        color: black;
    }
}
```

Note: make sure contrast is always good, even without this media query.

## Custom font

Define a custom font. All modern browsers support WOFF2.

```css
@font-face {
  font-family: MavenPro;
  src: url('fonts/mavenpro/maven_pro_bold-webfont.woff2') format('woff2');
  font-weight: bold;
  font-style: normal;
  font-display: swap;
}
```

## Font weights

Which font weight number belongs to which font weight name.

css | name
--- | ---
100 | Thin
300 | Light
350 | Book
400 (normal)| Normal/Regular
500 | Medium
600 | Semi Bold/Demi Bold
700 (bold)| Bold
800 | Extra Bold/Ultra Bold
900 | Black/Heavy

## Responsive design

Every webpage should look good on desktop, tablet and mobile.

```css
/* Mobile */
.box {
  padding: 10px;
}
/* Tablet */
@media screen and (min-width: 768px) {
  .box {
    padding: 40px;
  }
}
/* Desktop */
@media screen and (min-width: 1024px) {
    .box {
      padding: 80px;
    }
}
```

## UI colors

Adjust the styling of UI elements and interactions.

```css

div {
    accent-color: lime; /* Color of UI elements */
    caret-color: blue; /* Color of caret (text cursor) */
}

div::selection { /* Styling of selected text */
    color: black;
    background-color: orange;
}
```

## Dark mode

Switch your color scheme to match the light or dark mode of the user.

```css
html {
    color: black;
    background-color: white;
}
@media (prefers-color-scheme: dark) {
  html {
      color: white;
      background-color: black;
  }
}
```

If you have your own toggle, then don't forget to set the `color-scheme` property, so UI elements will adapt to the theme.

## CSS stylable icons

Change the color of svg's with CSS.
If you have multiple svg's, you can use [svg-sprite](https://www.npmjs.com/package/svg-sprite) to combine them
in one single svg using the _view_ mode.

```bash
npx svg-sprite --view --view-bust false --view-example --dest=dest assets/icons/*.svg
```

If one of your svg-files is called `mail.svg`, you can show the icon using this class:

```css
.mail-icon {
  width: 24px;
  height: 24px;
  background: currentColor;
  mask-image: url(dest/sprites.svg#mail);
  mask-size: contain;
}
```

In this case, the icon gets the same color as the surrounding text, but you can
apply any gradient or background image you want.

```html
<span class="mail-icon"></span>
```

## Truncate with ellipsis

Instead of wrapping a text, show an ellipsis (…)

```css
.text {
    width: 200px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
```

Use line clamp but for multiple lines.

```css
.box {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  overflow: hidden;
  -webkit-line-clamp: 3;
  line-clamp: 3;
}
```

## Remove button styles

Also works with other (ui) elements.

```css
button.my-style {
  padding: 0;
  border: none;
  background-color: transparent;
  /* my styles… */
}
```

You can also reset all styles. Note that this also removes your own inherited styles.

```css
button.my-style {
  all: initial;
  /* my styles… */
}
```

Use flexbox to show text at the top of the button, to make it exchangeable with a `<div>`.

```css
button.my-style {
  /* other reset styles… */
  display: inline-flex;
  align-items: flex-start;
  /* my styles… */
}
```

## Only show focus when applicable

Don't show focus outlines for mouse users. Note that `<input>` and `<textarea>` will always apply the `focus-visible` style.
Use `transparent` as a standard color, as this will become visible in high contrast mode.

```css
* {
  outline-color: transparent;
}

:focus-visible {
  outline: 1px solid #00A1F1;
}
```

## Conditional hover

Some devices like mobiles might not have hover and change the style to compensate.

```css
div {
    /* styles when hover is not supported */
}

@media (hover) {
    div {
        /* styles when hover is supported */
    }

    div:hover {
        /* styles with hover */
    }
}
```


## Use aria-label to provide "alt" for background image

> [!NOTE]  
> Don't include text in this element.

```html
<div class="background-image" role="img" aria-label="Alt text"></div>
```

The [aria-label attribute](https://html5accessibility.com/stuff/2024/05/22/not-so-short-note-on-aria-label-usage-big-table-edition/) has much more uses.

## Make icons searchable

Use `hidden="until-found"` to hide text until the user searches for it, recommended when using icons without text.

```html
<a href="/contact">
  <svg.../>
  <span hidden="until-found">Contact</span>
</a>
```

This feature is only supported in Chrome, but it's expected to be supported in all browsers in 2025.

See [Rethinking Find-in-Page Accessibility: Making Hidden Text Work for Everyone](https://schepp.dev/posts/rethinking-find-in-page-accessibility-making-hidden-text-work-for-everyone/)

## Remove semantics

Remove the semantics from an element

```html
<h2 role="presentation">Large text, but not a heading</h2>
```

## Current page

Don't highlight the current page in a table of contents by only changing the class but use `aria-current`.

```html
<ol>
    <li><a href="…">Some page</a></li>
    <li aria-current="page">Some other page</li>
</ol>
```

Then style the current page entry in the table as contents as follows

```css
[aria-current="page"] {
    font-weight: bold;
}
```

`aria-current` can have the following values: `page`, `step`, `location`, `date`, `time`, `true` and `false`.
See [MDN: aria-current](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-current) 
for a detailed explanation.

## Toggle buttons

Make it clear when buttons are toggled on or off.

```html
<ol role="tablist">
  <li><button role="tab" aria-selected="false">One</button></li>
  <li><button role="tab" aria-selected="true">Two</button></li>
</ol>
```

Then you can also use the `aria-selected` attribute for styling:

```css
[aria-selected='true'] {
    background-color: mintcream;
}
```

See also [WAI-ARIA Authoring Practices](https://www.w3.org/TR/wai-aria-practices/)

## Scrollbar styling

You can style the scrollbar, but this is very browser and operating system dependent,
so test where necessary.
Apply both classes (`scrollbar-style1` and `styled-scrollbar`) to your container.

```
/* Custom style with configurable parameters */
.scrollbar-style1 {
  overflow: auto; /* enable automatic scrollbars */
  scrollbar-width: thin; /* none, thin or auto (Firefox) */
  --scrollbar-size: 8px; /* 8px when using thin (Webkit) */
  --scrollbar-color: lightblue;
  --scrollbar-thumb-color: blue;
  --scrollbar-thumb-rect: 1; /* add this line for a rectangular thumb (Webkit) */
}

/* You can leave the code below as is */
.styled-scrollbar {
  scrollbar-color: var(--scrollbar-thumb-color) var(--scrollbar-color, transparent);
}

/* WebKit and Chromiums */
.styled-scrollbar::-webkit-scrollbar {
  width: var(--scrollbar-size);
  height: var(--scrollbar-size);
  background-color: var(--scrollbar-color);
}

.styled-scrollbar::-webkit-scrollbar-thumb {
  background: var(--scrollbar-thumb-color);
  border-radius: calc(99px - var(--scrollbar-thumb-rect, 0) * 99px);
}
```

## RSS feed

If your site has an RSS (or Atom) feed, make it discoverable for RSS readers.
Put the following code in your HTML head.

Example for an RSS feed:

```html
<link rel="alternate" type="application/rss+xml" title="My site name" href="https://example.com/feed.rss.xml" />
```

Example for an Atom feed:

```html
<link rel="alternate" type="application/atom+xml" title="My site name" href="https://example.com/feed.atom.xml" />
```

## Miscellaneous CSS properties

Handy properties that are hard to memorize but can sometimes be very useful.

| Property                            | Use                                                                      | More info                                                                                            |
|-------------------------------------|--------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| @layer                              | Organize your CSS                                                        | [MDN: @layer](https://developer.mozilla.org/en-US/docs/Web/CSS/@layer)                               |
| @container                          | Responsive elements                                                      | [MDN: @container](https://developer.mozilla.org/en-US/docs/Web/CSS/@container)                       |
| text-underline-offset: 0.25em       | Set the distance between the text and the underline                      | [MDN: text-underline-offset](https://developer.mozilla.org/en-US/docs/Web/CSS/text-underline-offset) |
| margin-block: 1lh                   | Set the margin for the top and bottom of an element                      | [MDN: margin-block](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-block)                   |
| margin-trim: block-start            | Trim the margin of an element                                            | [MDN: margin-trim](https://developer.mozilla.org/en-US/docs/Web/CSS/margin-trim)                     |
| scroll-margin-top: 2rem             | Set the scroll margin for the top of an element                          | [MDN: scroll-margin-top](https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-margin-top)         |
| overscroll-behavior: contain        | Prevent overscroll effects                                               | [MDN: overscroll-behavior](https://developer.mozilla.org/en-US/docs/Web/CSS/overscroll-behavior)     |
| scrollbar-gutter: stable both-edges | Set the scrollbar gutter                                                 | [MDN: scrollbar-gutter](https://developer.mozilla.org/en-US/docs/Web/CSS/scrollbar-gutter)           |
| width: fit-content                  | Set the width of an element to the width of its content                  | [MDN: width](https://developer.mozilla.org/en-US/docs/Web/CSS/width)                                 |
| aspect-ratio: 16 / 9                | Set the aspect ratio of an element                                       | [MDN: aspect-ratio](https://developer.mozilla.org/en-US/docs/Web/CSS/aspect-ratio)                   |
| object-fit: cover                   | Specify how an image should be shown in an `img` element                 | [MDN: object-fit](https://developer.mozilla.org/en-US/docs/Web/CSS/object-fit)                       |
| touch-action: manipulation          | Prevent click delay by not waiting for possible double click             | [MDN: touch-action](https://developer.mozilla.org/en-US/docs/Web/CSS/touch-action)                   |
| pointer-events: none                | Make a top level element behave like it's not there                      | [MDN: pointer-events](https://developer.mozilla.org/en-US/docs/Web/CSS/pointer-events)               |
| user-select: none                   | Prevents text to be selected                                             | [MDN: user-select](https://developer.mozilla.org/en-US/docs/Web/CSS/user-select)                     |
| display: contents                   | Remove the element from the document tree                                | [MDN: display](https://developer.mozilla.org/en-US/docs/Web/CSS/display)                             |
| isolation: isolate                  | Prevent the element from being affected by the z-index of other elements | [MDN: isolation](https://developer.mozilla.org/en-US/docs/Web/CSS/isolation)                         |
| content-visibility: hidden          | Hide elements that are not visible on screen                             | [MDN: content-visibility](https://developer.mozilla.org/en-US/docs/Web/CSS/content-visibility)       |
| contain: size layout paint style    | Prevent the element from affecting the layout of the page                | [MDN: contain](https://developer.mozilla.org/en-US/docs/Web/CSS/contain)                             |

## Checklist

Even when a site looks fine on first glance, it can still be broken.
Check the list below to make sure the site is really ready to be published.

- Check the site in Google Lighthouse and make sure the score is good
- Is the site SEO friendly? Can it be found with search engines?
- Test the site on various mobile devices (phones and tablets)
- Has a proper 404 page been set up for when a invalid url is requested?
- Some jurisdictions require contact/about/legal info pages
- The back button always goes to the previous page
- Is the text easy to read?
- Can you use the site with keyboard only?
- Does the site still work when the text is enlarged? (CTRL-+ or Command-+)
- Form fields use the autocomplete attribute
- Every page has a different title (with the generic part at the end)
- Don't forget the favicon
- Add an image and description for when the site is shared on social media
- Add a print style sheet for when it is expected the pages will be printed
- Add the lang attribute
- For international sites in one language: the site works with browser autotranslation

## Copy paste characters

Some symbols are hard to type and sometimes you want to know the HTML entity code.

name | entity code | character
--- | --- | ---
Degree sign| \&deg; | °
Horizontal ellipsis | \&hellip; | …
Bullet | \&bullet; | •
Multiplication sign | \&times; | ×
Euro sign | \&euro; | €
Single left quotation mark | \&lsquo; | ‘
Single right quotation mark | \&rsquo; | ’
Single low-9 quotation mark | \&lsquor; | ‚
Double left quotation mark  | \&ldquo; | “
Double right quotation mark | \&rdquo; | ”
Double low-9 quotation mark | \&ldquor; | „

See also [Character Entity Reference Chart](https://dev.w3.org/html5/html-author/charref)

## Lorem Ipsum

Copy and paste placeholder text.

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque varius sem sed nibh pharetra, id ultricies justo sodales. Integer convallis magna lobortis, pulvinar massa et, egestas risus. Nunc ultrices eget nibh convallis auctor. Sed at luctus felis, nec fringilla ante. Aenean facilisis urna eget pellentesque posuere. Maecenas faucibus sem sit amet diam euismod, mollis bibendum quam ornare. Quisque finibus arcu quis molestie pulvinar. Duis sed aliquam nibh, ut pharetra felis. Aenean vel fermentum risus, ac tincidunt enim. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Quisque elementum sit amet libero sed accumsan. Duis nec nunc nec dolor posuere pulvinar. Quisque suscipit congue mi, sed imperdiet libero laoreet non. In sed sodales neque, in bibendum lectus.

Ut nec posuere ipsum. Sed sagittis malesuada dui a blandit. Mauris consectetur consectetur laoreet. Sed erat quam, semper non euismod ut, consequat vitae neque. Sed sodales lorem quis erat iaculis, tristique varius diam tincidunt. Sed venenatis ipsum nec accumsan bibendum. Nulla ac felis sit amet ipsum feugiat viverra non eget erat. Maecenas enim nulla, vehicula eu purus id, lacinia tincidunt leo. Interdum et malesuada fames ac ante ipsum primis in faucibus. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Nulla facilisi. Aliquam suscipit interdum massa. Integer sit amet tincidunt nulla. Proin et ante felis. Pellentesque mauris orci, rutrum sed massa vel, lobortis consequat justo.
