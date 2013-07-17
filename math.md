Math
====

A very selective reference to javascript-based tools and techniques useful for creating geometric visualizations.

--- 

Javascript's built-in [Math](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math) object provides the primitives used to build higher-level abstractions.  


## Basic Trig

* [Math.PI](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/PI) - built-in constant, useful for converting between radians and degrees.

* [Math.cos(θ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/cos) - get `x` coordinate from angle `θ`.

* [Math.sin(θ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/sin) - get `y` coordinate from angle `θ`.

* [Math.atan2(y, x)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/atan2) - convert `x, y` coordinates to angle.

* [Math.atan(r)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/atan) - arctangent of `r`.  (`atan2` is passed separate `x` and `y` arguments. You need to pass the *ratio* of those two arguments to `atan`.)

Note that the trig functions taking angle arguments are expected to be in [radian](http://en.wikipedia.org/wiki/Radian) units, not degrees.  (Recall that an arc of a circle with the same length as the radius of that circle corresponds to an angle of 1 radian. A full circle corresponds to an angle of 2π radians.)

    deg2rad = (d) -> deg * Math.PI/180


## Tutorials

* [Math for Pictures](http://macwright.org/2013/03/05/math-for-pictures.html)


## Resources

* [coffee-matrix](https://github.com/yizzreel/coffee-matrix) - affine transform matrix 

* [simple-statistics](https://github.com/tmcw/simple-statistics) - by Tom MacWright

* [science.js](https://github.com/jasondavies/science.js/) - by Jason Davies

* [numeric.js](https://github.com/sloisel/numeric/) - linear algebra library

* [sylvester.js](https://github.com/jcoglan/sylvester) - linear algebra library

* [versor.js](https://github.com/weshoke/versor.js) - JS port of [vsr](https://github.com/wolftype/vsr)


