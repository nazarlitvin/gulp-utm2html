Gulp-utm2html is a tool that will help add UTM tags to URL in HTML file. I use this plugin to make URL with UTM tags in my HTML emails.

##Usage

First, install gulp-utm2html as a development dependency:
```shell
npm install --save-dev gulp-utm2html
```

Then, add it to your gulpfile.js:

```shell
var gulp      = require('gulp'),
    utm2html  = require('gulp-utm2html');

gulp.task('default', function() {
    return gulp.src(['./*.html'])
        .pipe(utm2html({
            source: 'source',
            medium: 'medium',
            campaign: 'campaign',
            term: 'term',
            content: 'content'}))
        .pipe(gulp.dest('./dest')) });
```
Source, medium and campaign are essential parameters. Term and content are optional.

URL with mailto protocol will be ignored. If your URL already have UTM tags they will be replaced. To save exist UTM tags, or leave URL without UTM tags - use data-utm="nope" attribute like this:

```shell
<a href="https://github.com/nazarlitvin?utm_source=news&amp;utm_medium=email&amp;utm_campaign=speaker" data-utm="nope">
```

##Example

```shell
<a href="https://github.com/nazarlitvin">
	UTM tags will be added</a>
<a href="https://github.com/nazarlitvin?utm_source=tag&utm_medium=tag&utm_campaign=tag&utm_term=tag&utm_content=tag">
	UTM tags will be replaced</a>
<a href="https://github.com/nazarlitvin" data-utm="nope">
	URL will be ignored.</a>
<a href="https://github.com/nazarlitvin?utm_source=tag&utm_medium=tag&utm_campaign=tag&utm_term=tag&utm_content=tag" data-utm="nope">
	UTM tags will be saved.</a>
<a href="mailto:n.litvin41@gmail.com">
	URL with mailto protocol will be ignored.</a>
<a href="tel:07700900000">
	URL with tel protocol will be ignored.</a>
```

This code will compiled to this:

```shell
<a href="https://github.com/nazarlitvin?utm_source=source&utm_medium=medium&utm_campaign=campaign&utm_term=term&utm_content=content">
	UTM tags will be added</a>
<a href="https://github.com/nazarlitvin?utm_source=source&utm_medium=medium&utm_campaign=campaign&utm_term=term&utm_content=content">
	UTM tags will be replaced</a>
<a href="https://github.com/nazarlitvin" data-utm="nope">
	URL will be ignored.</a>
<a href="https://github.com/nazarlitvin?utm_source=tag&utm_medium=tag&utm_campaign=tag&utm_term=tag&utm_content=tag" data-utm="nope">
	UTM tags will be saved.</a>
<a href="mailto:n.litvin41@gmail.com">
	URL with mailto protocol will be ignored.</a>
<a href="tel:07700900000">
	URL with tel protocol will be ignored.</a>
```

MIT License
