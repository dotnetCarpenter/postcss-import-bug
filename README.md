# postcss-import bug

The `<` sign inside a CSS comment is transpiled to `\3c ` which breaks our live UI documentation.

Link to post-import issue: https://github.com/postcss/postcss-import/issues/595


### Minimal reproducible repo

Example CSS:

```css
/*
<div class="f-content"> \3c !-- only here for the style guide - should not be used on the website -->
*/
body {
    background-color: black;
}
```

With the following _package.json_:

```json
"scripts": {
    "bug": "postcss --no-map --use postcss-import -o main.css css/*.css",
    "build": "postcss --no-map --o main.css css/*.css"
}
```

If you run `npm run bug && cat main.css` you will get:

```css
/*
<div class="f-content"> \3c !-- only here for the style guide - should not be used on the website -->
*/
body {
    background-color: black;
}
```

Running `npm run build && cat main.css`you will get:
```css
/*
<div class="f-content"> <!-- only here for the style guide - should not be used on the website -->
*/
body {
    background-color: black;
}
```
