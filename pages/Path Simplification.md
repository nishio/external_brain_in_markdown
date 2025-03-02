
[https://github.com/paperjs/paper.js/blob/c7d85b663edb728ec78fffa9f828435eaf78d9c9/src/path/Path.js#L1280](https://github.com/paperjs/paper.js/blob/c7d85b663edb728ec78fffa9f828435eaf78d9c9/src/path/Path.js#L1280)
js

```javascript
simplify: function(tolerance) {
        var segments = new PathFitter(this).fit(tolerance || 2.5);
        if (segments)
            this.setSegments(segments);
        return !!segments;
    },
```


[https://github.com/paperjs/paper.js/blob/15e00e0b99b5f59215028826a39321248f433d7a/src/path/PathFitter.js](https://github.com/paperjs/paper.js/blob/15e00e0b99b5f59215028826a39321248f433d7a/src/path/PathFitter.js)

// An Algorithm for Automatically Fitting Digitized Curves
// by Philip J. Schneider
// from "Graphics Gems", Academic Press, 1990
// Modifications and optimizations of original algorithm by Juerg Lehni.

> maxError = Math.max(error, error * error),

[https://github.com/paperjs/paper.js/blob/15e00e0b99b5f59215028826a39321248f433d7a/src/path/PathFitter.js#L273](https://github.com/paperjs/paper.js/blob/15e00e0b99b5f59215028826a39321248f433d7a/src/path/PathFitter.js#L273)

ts

```typescript
    findMaxError: function(first, last, curve, u) {
        var index = Math.floor((last - first + 1) / 2),
            maxDist = 0;
        for (var i = first + 1; i < last; i++) {
            var P = this.evaluate(3, curve, u[i - first]);
            var v = P.subtract(this.points[i]);
            var dist = v.x * v.x + v.y * v.y; // squared
            if (dist >= maxDist) {
                maxDist = dist;
                index = i;
            }
        }
        return {
            error: maxDist,
            index: index
        };
    }
```


