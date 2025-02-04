# schrodinger-1d

> [The Schrödinger Equation with a potential barrier in 1D](https://rreusser.github.io/demos/schrodinger-1d/)

[![experimental][stability-experimental]][stability-url]
<!--[![Build Status][travis-image]][travis-url]-->
<!--[![npm version][npm-image]][npm-url]-->
<!--[![Dependency Status][david-dm-image]][david-dm-url]-->
<!--[![Semistandard Style][semistandard-image]][semistandard-url]-->


## Introduction

This demo solves [Schrödinger's Equation](https://en.wikipedia.org/wiki/Schr%C3%B6dinger_equation) in the presence of a potential. That is, <p align="center"><img alt="i&bsol;hbar &lcub;&bsol;frac &lcub;&bsol;partial &rcub;&lcub;&bsol;partial t&rcub;&rcub;&bsol;Psi &lpar;&bsol;mathbf &lcub;r&rcub; &comma;t&rpar;&equals;&bsol;left&lsqb;&lcub;&bsol;frac &lcub;-&bsol;hbar &Hat;&lcub;2&rcub;&rcub;&lcub;2&bsol;mu &rcub;&rcub;&bsol;nabla &Hat;&lcub;2&rcub;&plus;V&lpar;&bsol;mathbf &lcub;r&rcub; &comma;t&rpar;&bsol;right&rsqb;&bsol;Psi &lpar;&bsol;mathbf &lcub;r&rcub; &comma;t&rpar;" valign="middle" src="images/ihbar-frac-partial-partial-tpsi-mathbf-r-tlef-d4cf84b0b7.png" width="356.5" height="55"></p> with `hbar = 1` and `µ = 1`. (Actually, please don't rely on the scale factors! I haven't carefully verified them since they don't affect the behavior to within a constant multiple of the inputs.)

This simulation uses [RK-4](https://github.com/scijs/ode-rk4) temporal integration and spectral differentiation (differentiation via the [FFT](https://github.com/scijs/ndarray-fft)) in space. Spectral derivatives resolve wavenumbers perfectly, as opposed to typical second order finite differences which tend to lead to heavy dispersion. The boundary conditions are implemented using the Perfectly Matched Layer (PML) of Berenger [1].

## Examples

- [Reflection and transmission across a potential barrier](https://rreusser.github.io/demos/schrodinger-1d/#integration=%7B%22dt%22%3A0.0001%2C%22stepsPerIter%22%3A5%2C%22method%22%3A%22rk4%22%7D&pml=%7B%22width%22%3A0.05%2C%22exponent%22%3A1%2C%22gamma%22%3A1.5707963267948966%7D&potential=%7B%22width%22%3A0.1%2C%22magnitude%22%3A1000%2C%22inverted%22%3Afalse%2C%22center%22%3A1%2C%22exponent%22%3A2%7D&pulse=%7B%22center%22%3A0.5%2C%22width%22%3A0.1%2C%22magnitude%22%3A1%2C%22wavenumber%22%3A200%7D&pulse2=%7B%22center%22%3A1.5%2C%22width%22%3A0.1%2C%22magnitude%22%3A0%2C%22wavenumber%22%3A-200%7D)
- [Spreading of the wave packet (higher-frequency components move faster)](https://rreusser.github.io/demos/schrodinger-1d/#integration=%7B%22dt%22%3A0.0001%2C%22stepsPerIter%22%3A5%2C%22method%22%3A%22rk4%22%7D&pml=%7B%22width%22%3A0.05%2C%22exponent%22%3A1%2C%22gamma%22%3A1.5707963267948966%7D&potential=%7B%22width%22%3A0.1%2C%22magnitude%22%3A0%2C%22inverted%22%3Afalse%2C%22center%22%3A1%2C%22exponent%22%3A1.98%7D&pulse=%7B%22center%22%3A0.5%2C%22width%22%3A0.012%2C%22magnitude%22%3A1%2C%22wavenumber%22%3A400%7D&pulse2=%7B%22center%22%3A1.5%2C%22width%22%3A0.1%2C%22magnitude%22%3A0%2C%22wavenumber%22%3A-200%7D)
- [Bouncing in a potential well](https://rreusser.github.io/demos/schrodinger-1d/#integration=%7B%22dt%22%3A0.0001%2C%22stepsPerIter%22%3A5%2C%22method%22%3A%22rk4%22%7D&pml=%7B%22width%22%3A0.05%2C%22exponent%22%3A1%2C%22gamma%22%3A1.5707963267948966%7D&potential=%7B%22width%22%3A0.7%2C%22magnitude%22%3A5000%2C%22inverted%22%3Atrue%2C%22center%22%3A1%2C%22exponent%22%3A50%7D&pulse=%7B%22center%22%3A1%2C%22width%22%3A0.106%2C%22magnitude%22%3A1%2C%22wavenumber%22%3A220%7D&pulse2=%7B%22center%22%3A1.5%2C%22width%22%3A0.1%2C%22magnitude%22%3A0%2C%22wavenumber%22%3A-200%7D)

<p align="center">
  <a href="https://rreusser.github.io/demos/schrodinger-1d/">
    <img src="images/sample.gif" alt="Reflection and transmission from a potential barrier">
  </a>
</p>

[View demo →](https://rreusser.github.io/demos/schrodinger-1d/)

In the demo, the blue and green lines are the real and imaginary components of the wavefunction, with the envelope displayed in black. The red represents the potential barrier with scale displayed on the right, and the gray represents the perfectly matched layer which suppresses reflections.

## To Do

- Verify and tighten up the constant scale factors

## References

[1] Berenger, J.-P. "[A Perfectly Matched Layer for the Absorption of Electromagnetic Waves](http://web.stanford.edu/class/ee256/Berenger1994.pdf)", Journal of Computational Physics. 114, 185-200 (1994).

## License

&copy; 2016 Ricky Reusser. MIT License.




<!-- BADGES -->

[travis-image]: https://travis-ci.org/rreusser/demos/schrodinger-1d.svg?branch=master
[travis-url]: https://travis-ci.org//demos/schrodinger-1d

[npm-image]: https://badge.fury.io/js/demos/schrodinger-1d.svg
[npm-url]: https://npmjs.org/package/demos/schrodinger-1d

[david-dm-image]: https://david-dm.org/rreusser/demos/schrodinger-1d.svg?theme=shields.io
[david-dm-url]: https://david-dm.org/rreusser/demos/schrodinger-1d

[semistandard-image]: https://img.shields.io/badge/code%20style-semistandard-brightgreen.svg?style=flat-square
[semistandard-url]: https://github.com/Flet/semistandard

<!-- see stability badges at: https://github.com/badges/stability-badges -->
[stability-url]: https://github.com/badges/stability-badges
[stability-deprecated]: http://badges.github.io/stability-badges/dist/deprecated.svg
[stability-experimental]: http://badges.github.io/stability-badges/dist/experimental.svg
[stability-unstable]: http://badges.github.io/stability-badges/dist/unstable.svg
[stability-stable]: http://badges.github.io/stability-badges/dist/stable.svg
[stability-frozen]: http://badges.github.io/stability-badges/dist/frozen.svg
[stability-locked]: http://badges.github.io/stability-badges/dist/locked.svg
