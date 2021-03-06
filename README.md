`gulp-jspm` wraps the `jspm bundle moduleName` command line.

### Usage

```js
var gulp = require('gulp');
var gulp_jspm = require('gulp-jspm'); // npm install gulp-jspm

gulp.task('default', function(){
    return gulp.src('src/main.js')
        .pipe(gulp_jspm())
        .pipe(gulp.dest('build/'));
});
```

This will generate the `demo/build/jspm-bundle.js` file.
This file corresponds to the file generated by the command `jspm bundle main`.

Many code snippets shown in this Readme are implemented at [demo/gulpfile.js](demo/gulpfile.js).



###### Before Opening an Issue

When opening an issue, copy the debug logs in the ticket.
The debug logs are printed when running `gulp-jspm` with the verbose option `gulp_jspm({verbose: true})`.



###### Source Map

```js
var sourcemaps = require('gulp-sourcemaps');

gulp.src('src/main.js')
    .pipe(sourcemaps.init())
    .pipe(gulp_jspm())
    .pipe(sourcemaps.write('.'))
    .pipe(gulp.dest('build/'));
```


###### Options

```js
// exclude message.js from bundle
gulp.src('src/main.js')
    .pipe(gulp_jspm({arithmetic: '- message'}))
    .pipe(gulp.dest('build/'));

// `jspm bundle-sfx main`
gulp.src('src/main.js')
    .pipe(gulp_jspm({selfExecutingBundle: true}))
    .pipe(gulp.dest('build/'));

// `jspm bundle main.jsx!`
gulp.src('src/main.jsx')
    .pipe(gulp_jspm({plugin: true}))
    .pipe(gulp.dest('build/'));

// `jspm bundle main.jsx!jsx`
gulp.src('src/main.jsx')
    .pipe(gulp_jspm({plugin: 'jsx'}))
    .pipe(gulp.dest('build/'));

// print information logs about the internal progress of `gulp-jspm`
gulp.src('src/main.js')
    .pipe(gulp_jspm({verbose: true}))
    .pipe(gulp.dest('build/'));

// All other options given to gulp-jspm are passed on to jspm.
// All jspm options can therefore be passed to `gulp-jspm`
// (`minify`, `mangle`, `lowResSourceMaps`, etc.).
// For example:
gulp.src('src/main.js')
    .pipe(gulp_jspm({inject: true})) // `jspm bundle main --inject`
    .pipe(gulp.dest('build/'));
```


###### Original Entry Point

```js
gulp.src('src/main.js')
    .pipe(gulp_jspm())
    .pipe(pass(function(vinyl_file){
        assert( vinyl_file.relative === 'main.bundle.js' );
        assert( vinyl_file.originalEntryPoint.relative === 'main.js' );
    }));
```


### Run Gulpfile Demo

To run the code snippets above execute following commands.

```js
git clone git@github.com:brillout/gulp-jspm
cd gulp-jspm/
npm install
cd demo/
npm install
npm install -g jspm
npm install -g gulp
jspm install
gulp
gulp sourcemap
gulp test
```

