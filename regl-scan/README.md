# [WIP] regl-scan

> GPU Scan (generalized prefix-sum) via regl

## Introduction

Applies a [scan (prefix-sum)](https://en.wikipedia.org/wiki/Prefix_sum) operation to a [regl](https://github.com/regl-project/regl) framebuffer. It's very similar to map-reduce except each output component contains a partial result. This repo implements the basic algorithm in GLSL, subject to the limitation that it only deals in 2D four-component textures of type `uint8` or `float32`.

## Example

<a href="https://rreusser.github.io/demos/regl-scan/"><img src="./screenshot.png"></a>

See: [live summed area table](https://rreusser.github.io/demos/regl-scan/)

To compute a [summed area table](https://en.wikipedia.org/wiki/Summed_area_table) for each component independently:

```javscript
const prefixSum = require('./)(regl, {
  reduce: `vec4 reduce(vec4 prefix, vec4 sum) {
    return prefix + sum;
  }`
});

var result = prefixSum({src: srcFbo, dest: destFbo, axis: 0});
result = prefixSum({src: result.dest, dest: result.src, axis: 1});
// => answer in result.dest
```

where `srcFbo` and `destFbo` are [regl framebuffers](https://github.com/regl-project/regl). You can never write to the same framebuffer, so the algorithm ping-pongs between two framebuffers. As a result, it's not certain which framebuffer will contain the result at the end. To save an unnecessary copy operation, the result contains the framebuffer receiving the final output in `result.dest` and the scratch buffer in `result.src`.

Or to compute a summed area table for a input vector containing adjacent `xyzw` vectors:

```javscript
const prefixSum = require('./)(regl, {
  map: `vec4 map(vec4 f) {
    // Prefix-sum for this vec4:
    f.yzw += f.xyz;
    f.zw += f.xy;
    return f;
  }
  reduce: `vec4 reduce(vec4 prefix, vec4 sum) {
    // Only care about the *last* component of the prefix:
    return vec4(prefix.w) + sum;
  }`
});

var result = prefixSum({src: srcFbo, dest: destFbo, axis: 0});
result = prefixSum({src: result.dest, dest: result.src, axis: 1});
// => answer in result.dest
```

## See also

- [ndarray-prefix-sum](https://github.com/scijs/ndarray-prefix-sum)

## License

&copy; Ricky Reusser 2016. MIT License.
