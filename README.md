gulp-md-docs
=====================
Building navigable HTML documentation from *.md files with code syntax highlighting (via highlight.js), navigation menu and flexible template.

# Installation

```bash
$ npm install gulp-md-docs
```

# Usage

## Copy template folder

`./doc_src`

## Require template settings

``` js
var docTemplate = require('./doc_src/index.js');
```

## Add task for copy template static files and folder to doc dist

``` js
gulp.task('copy_template_root_dir', function() {
    return gulp.src(docTemplate.root_dir + '/**/*')
        .pipe(copy())
        .pipe(gulp.dest('doc_dist'));
});
```

## Add task for compile doc

``` js
gulp.task('compile_doc', function() {
    return gulp.src('doc_md/**/*.md')
        .pipe(gulpMdDocs({
            template: docTemplate
        }))
        .pipe(gulp.dest('doc_dist'));
});
```

---

gulpfile.js

```js
var gulp = require('gulp');
var gulpMdDocs = require('gulp-md-docs');
var copy = require('gulp-contrib-copy');

var docTemplate = require('./doc_src/index.js');

gulp.task('copy_template_root_dir', function() {
    return gulp.src(docTemplate.root_dir + '/**/*')
        .pipe(copy())
        .pipe(gulp.dest('doc_dist'));
});

gulp.task('compile_doc', function() {
    return gulp.src('doc_md/**/*.md')
        .pipe(gulpMdDocs({
            template: docTemplate
        }))
        .pipe(gulp.dest('doc_dist'));
});

gulp.task('default', ['copy_template_root_dir', 'compile_doc']);

gulp.task('watch', function() {
    gulp.watch('example/**/*.md', ['copy_template_root_dir', 'compile_doc']);
});

```
