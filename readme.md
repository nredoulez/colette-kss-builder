# Colette kss-builder

Custom Twig.js builder for [kss-node](https://github.com/kss-node/kss-node) designed for [Colette](https://github.com/20minutes/colette).

## Custom KSS rules added

KSS is great but some options are missing.

### Colors

To document colors

```scss
// Colors
//
// Color pallet
//
// Colors:
// $color-base:         #4c4d4e - text color
// $color-base-lighten: #e7e7e7 - lighten version
// $color-secondary:    #b7b7b7 - secondary text color
// $color-tertiary:     #878787 - tertiary text color
// $color-links:        #0091aa - links color
//
// Style guide: Colors
```

### Symbols

To document SVG symbols

```scss
// SVG symbols
//
// A collection of svg symbols built with [svgstore](https://www.npmjs.com/package/svgstore).
//
// Symbols: **/*.svg in ../../svg/
//
// Style guide: Symbols
```

A new option is added to KSS to include SVG symbols bundle in KSS template.

```json
{
  "svg": "dist/assets/svg/svg.svg"
}
```

This gulp task can build your SVG symbols pack

```js
const gulp = require('gulp')
const rename = require('gulp-rename')
const svgstore = require('gulp-svgstore')

gulp.task('svg', function () {
  return gulp
    .src('src/svg/**/*', { base: 'src/svg'})
    .pipe(rename((filePath) => {
      const name = filePath.dirname !== '.' ? filePath.dirname.split(filePath.sep) : [];
      name.push(filePath.basename)
      filePath.basename = `symbol-${name.join('-')}`
    }))
    .pipe(svgstore({ inlineSvg: true }))
    .pipe(gulp.dest('dist/assets/svg/));
}
```
