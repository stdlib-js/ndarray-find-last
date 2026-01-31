<!--

@license Apache-2.0

Copyright (c) 2026 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# findLast

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Return a new [ndarray][@stdlib/ndarray/ctor] containing the last elements which pass a test implemented by a predicate function along one or more [ndarray][@stdlib/ndarray/ctor] dimensions.

<section class="intro">

</section>

<!-- /.intro -->



<section class="usage">

## Usage

To use in Observable,

```javascript
findLast = require( 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-find-last@umd/browser.js' )
```
The previous example will load the latest bundled code from the umd branch. Alternatively, you may load a specific version by loading the file from one of the [tagged bundles](https://github.com/stdlib-js/ndarray-find-last/tags). For example,

```javascript
findLast = require( 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-find-last@v0.1.0-umd/browser.js' )
```

To vendor stdlib functionality and avoid installing dependency trees for Node.js, you can use the UMD server build:

```javascript
var findLast = require( 'path/to/vendor/umd/ndarray-find-last/index.js' )
```

To include the bundle in a webpage,

```html
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-find-last@umd/browser.js"></script>
```

If no recognized module system is present, access bundle contents via the global scope:

```html
<script type="text/javascript">
(function () {
    window.findLast;
})();
</script>
```

#### findLast( x\[, options], predicate\[, thisArg] )

Returns a new [ndarray][@stdlib/ndarray/ctor] containing the last elements which pass a test implemented by a predicate function along one or more [ndarray][@stdlib/ndarray/ctor] dimensions.

<!-- eslint-disable no-invalid-this, max-len -->

```javascript
var array = require( '@stdlib/ndarray-array' );

function isEven( value ) {
    return value % 2.0 === 0.0;
}

// Create an input ndarray:
var x = array( [ [ [ 1.0, 2.0 ], [ 3.0, 4.0 ] ], [ [ 5.0, 6.0 ], [ 7.0, 8.0 ] ] ] );
// returns <ndarray>

// Perform reduction:
var out = findLast( x, isEven );
// returns <ndarray>[ 8.0 ]
```

The function accepts the following arguments:

-   **x**: input [ndarray][@stdlib/ndarray/ctor].
-   **options**: function options _(optional)_.
-   **predicate**: predicate function.
-   **thisArg**: predicate function execution context _(optional)_.

The function accepts the following options:

-   **dims**: list of dimensions over which to perform a reduction.
-   **keepdims**: boolean indicating whether the reduced dimensions should be included in the returned [ndarray][@stdlib/ndarray/ctor] as singleton dimensions. Default: `false`.
-   **sentinel**: value to return when no element passes the test. May be either a scalar value or a zero-dimensional [ndarray][@stdlib/ndarray/ctor].

By default, the function performs reduction over all elements in a provided [ndarray][@stdlib/ndarray/ctor]. To reduce specific dimensions, set the `dims` option.

<!-- eslint-disable max-len -->

```javascript
var array = require( '@stdlib/ndarray-array' );

function isEven( value ) {
    return value % 2.0 === 0.0;
}

// Create an input ndarray:
var x = array( [ [ [ 1.0, 2.0 ], [ 3.0, 4.0 ] ], [ [ 5.0, 6.0 ], [ 7.0, 8.0 ] ] ] );
// returns <ndarray>

var opts = {
    'dims': [ 0 ]
};

// Perform reduction:
var out = findLast( x, opts, isEven );
// returns <ndarray>[ [ NaN, 6.0 ], [ NaN, 8.0 ] ]
```

By default, the function returns an [ndarray][@stdlib/ndarray/ctor] having a shape matching only the non-reduced dimensions of the input [ndarray][@stdlib/ndarray/ctor] (i.e., the reduced dimensions are dropped). To include the reduced dimensions as singleton dimensions in the output [ndarray][@stdlib/ndarray/ctor], set the `keepdims` option to `true`.

<!-- eslint-disable max-len -->

```javascript
var array = require( '@stdlib/ndarray-array' );

function isEven( value ) {
    return value % 2.0 === 0.0;
}

// Create an input ndarray:
var x = array( [ [ [ 1.0, 2.0 ], [ 3.0, 4.0 ] ], [ [ 5.0, 6.0 ], [ 7.0, 8.0 ] ] ] );
// returns <ndarray>

var opts = {
    'dims': [ 0 ],
    'keepdims': true
};

// Perform reduction:
var out = findLast( x, opts, isEven );
// returns <ndarray>[ [ [ NaN, 6.0 ], [ NaN, 8.0 ] ] ]
```

To specify a custom sentinel value to return when no element passes the test, set the `sentinel` option.

<!-- eslint-disable max-len -->

```javascript
var array = require( '@stdlib/ndarray-array' );

function isEven( value ) {
    return value % 2.0 === 0.0;
}

// Create an input ndarray:
var x = array( [ [ [ 1.0, 3.0 ], [ 5.0, 7.0 ] ], [ [ 9.0, 11.0 ], [ 13.0, 15.0 ] ] ] );
// returns <ndarray>

var opts = {
    'sentinel': -999
};

// Perform reduction:
var out = findLast( x, opts, isEven );
// returns <ndarray>[ -999 ]
```

To set the `predicate` function execution context, provide a `thisArg`.

<!-- eslint-disable no-invalid-this, max-len -->

```javascript
var array = require( '@stdlib/ndarray-array' );

function isEven( value ) {
    this.count += 1;
    return value % 2.0 === 0.0;
}

// Create an input ndarray:
var x = array( [ [ [ 1.0, 2.0 ], [ 3.0, 4.0 ] ], [ [ 5.0, 6.0 ], [ 7.0, 8.0 ] ] ] );
// returns <ndarray>

var ctx = {
    'count': 0
};

// Perform reduction:
var out = findLast( x, isEven, ctx );
// returns <ndarray>[ 8.0 ]

var count = ctx.count;
// returns 1
```

#### findLast.assign( x, out\[, options], predicate\[, thisArg] )

Finds the last elements which pass a test implemented by a predicate function along one or more [ndarray][@stdlib/ndarray/ctor] dimensions and assigns results to a provided output [ndarray][@stdlib/ndarray/ctor].

<!-- eslint-disable max-len -->

```javascript
var array = require( '@stdlib/ndarray-array' );
var empty = require( '@stdlib/ndarray-empty' );
var getDType = require( '@stdlib/ndarray-dtype' );

function isEven( value ) {
    return value % 2.0 === 0.0;
}

// Create an input ndarray:
var x = array( [ [ [ 1.0, 2.0 ], [ 3.0, 4.0 ] ], [ [ 5.0, 6.0 ], [ 7.0, 8.0 ] ] ] );
// returns <ndarray>

// Create an output ndarray:
var y = empty( [], {
    'dtype': getDType( x )
});

// Perform reduction:
var out = findLast.assign( x, y, isEven );
// returns <ndarray>[ 8.0 ]

var bool = ( out === y );
// returns true
```

The function accepts the following arguments:

-   **x**: input [ndarray][@stdlib/ndarray/ctor].
-   **out**: output [ndarray][@stdlib/ndarray/ctor].
-   **options**: function options _(optional)_.
-   **predicate**: predicate function.
-   **thisArg**: predicate function execution context _(optional)_.

The function accepts the following options:

-   **dims**: list of dimensions over which to perform a reduction.
-   **sentinel**: value to return when no element passes the test. May be either a scalar value or a zero-dimensional [ndarray][@stdlib/ndarray/ctor].

<!-- eslint-disable max-len -->

```javascript
var array = require( '@stdlib/ndarray-array' );
var empty = require( '@stdlib/ndarray-empty' );
var getDType = require( '@stdlib/ndarray-dtype' );

function isEven( value ) {
    return value % 2.0 === 0.0;
}

// Create an input ndarray:
var x = array( [ [ [ 1.0, 2.0 ], [ 3.0, 4.0 ] ], [ [ 5.0, 6.0 ], [ 7.0, 8.0 ] ] ] );
// returns <ndarray>

// Create an output ndarray:
var y = empty( [ 2, 2 ], {
    'dtype': getDType( x )
});

var opts = {
    'dims': [ 0 ]
};

// Perform reduction:
var out = findLast.assign( x, y, opts, isEven );
// returns <ndarray>[ [ NaN, 6.0 ], [ NaN, 8.0 ] ]

var bool = ( out === y );
// returns true
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   By default, when no `sentinel` is provided, the function returns a default sentinel value based on the input [ndarray][@stdlib/ndarray/ctor] [data-type][@stdlib/ndarray/dtypes]:

    -   real-valued floating-point data types: `NaN`.
    -   complex-valued floating-point data types: `NaN + NaNj`.
    -   integer data types: maximum value.
    -   boolean data types: `false`.

-   The `predicate` function is provided the following arguments:

    -   **value**: current array element.
    -   **indices**: current array element indices.
    -   **arr**: the input [ndarray][@stdlib/ndarray/ctor].

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```html
<!DOCTYPE html>
<html lang="en">
<body>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/random-uniform@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/assert-is-positive-number@umd/browser.js"></script>
<script type="text/javascript">
(function () {.isPrimitive;
var ndarray2array = require( '@stdlib/ndarray-to-array' );
var findLast = require( '@stdlib/ndarray-find-last' );

var x = uniform( [ 2, 4, 5 ], -10.0, 10.0, {
    'dtype': 'float64'
});
console.log( ndarray2array( x ) );

var y = findLast( x, isPositive );
console.log( y.get() );

})();
</script>
</body>
</html>
```

</section>

<!-- /.examples -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/ndarray-find-last.svg
[npm-url]: https://npmjs.org/package/@stdlib/ndarray-find-last

[test-image]: https://github.com/stdlib-js/ndarray-find-last/actions/workflows/test.yml/badge.svg?branch=v0.1.0
[test-url]: https://github.com/stdlib-js/ndarray-find-last/actions/workflows/test.yml?query=branch:v0.1.0

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/ndarray-find-last/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/ndarray-find-last?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/ndarray-find-last.svg
[dependencies-url]: https://david-dm.org/stdlib-js/ndarray-find-last/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/ndarray-find-last/tree/deno
[deno-readme]: https://github.com/stdlib-js/ndarray-find-last/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/ndarray-find-last/tree/umd
[umd-readme]: https://github.com/stdlib-js/ndarray-find-last/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/ndarray-find-last/tree/esm
[esm-readme]: https://github.com/stdlib-js/ndarray-find-last/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/ndarray-find-last/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/ndarray-find-last/main/LICENSE

[@stdlib/ndarray/ctor]: https://github.com/stdlib-js/ndarray-ctor/tree/umd

[@stdlib/ndarray/dtypes]: https://github.com/stdlib-js/ndarray-dtypes/tree/umd

<!-- <related-links> -->

<!-- </related-links> -->

</section>

<!-- /.links -->
