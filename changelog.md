Arraymancer v0.3.0
==========================

I am very excited to announce the second release of Arraymancer which includes numerous improvements and breaking changes.
WARNING: Deprecated proc will be removed in a new release in a week due to deprecated spam.

Note:
- zeros, ones, newTensor

- **Very** Breaking
  - Tensors uses reference semantics now: `let a = b` will share data by default and copies must be made explicitly.
    - There is no need to use `unsafe` proc to avoid copies especially for slices.
    - Unsafe procs are deprecated and will be removed leading to a smaller and simpler codebase and API/documentation.
    - Tensors and CudaTensors now works the same way.
    - Use `clone` to do copies.
    - Arraymancer now works like Numpy and Julia, making it easier to port code.
    - Unfortunately it makes it harder to debug unexpected data sharing.

- Breaking ?
  - The max number of dimensions supported has been reduced from 8 to 7 to reduce cache misses.
    Note, in deep learning the max number of dimensions needed is 6 for 3D videos: [batch, time, color/feature channels, Depth, Height, Width]

- Deprecated
  - Version 0.3.1 with the ALL deprecated proc removed will be released in a week. Due to issue https://github.com/nim-lang/Nim/issues/6436,
    even using non-deprecated proc like `zeros`, `ones`, `newTensor` you will get a deprecated warning.
  - `newTensor`, `zeros`, `ones` arguments have been changed from `zeros([5, 5], int)` to `zeros[int]([5, 5])`
  - All `unsafe` proc are now default and deprecated.


- Cuda:
  - Support for convolution forward and backward


Arraymancer v0.2.0 Sept. 24, 2017 "The Color of Magic"
===========================================

I am very excited to announce the second release of Arraymancer which includes numerous improvements `blablabla` ...

Without further ado:
- Communauty
   - There is a Gitter room!
- Breaking
   - `shallowCopy` is now `unsafeView` and accepts `let` arguments
   - Element-wise multiplication is now `.*` instead of `|*|`
   - vector dot product is now `dot` instead of `.*`
- Deprecated
   - All tensor initialization proc have their `Backend` parameter deprecated.
   - `fmap` is now `map`
   - `agg` and `agg_in_place` are now `fold` and nothing (too bad!)

- Initial support for Cuda !!!
   - All linear algebra operations are supported
   - Slicing (read-only) is supported
   - Transforming a slice to a new contiguous Tensor is supported
- Tensors
   - Introduction of `unsafe` operations that works without copy: `unsafeTranspose`, `unsafeReshape`, `unsafebroadcast`, `unsafeBroadcast2`, `unsafeContiguous`, 
   - Implicit broadcasting via `.+, .*, ./, .-` and their in-place equivalent `.+=, .-=, .*=, ./=`
   - Several shapeshifting operations: `squeeze`, `at` and their `unsafe` version.
   - New property: `size`
   - Exporting: `export_tensor` and `toRawSeq`
   - Reduce and reduce on axis
- Ecosystem:
   - I express my deep thanks to @edubart for testing Arraymancer, contributing new functions, and improving its overall performance. He built [arraymancer-demos](https://github.com/edubart/arraymancer-demos) and [arraymancer-vision](https://github.com/edubart/arraymancer-vision),check those out you can load images in Tensor and do logistic regression on those!

Also thanks to the Nim communauty on IRC/Gitter, they are a tremendous help (yes Varriount, Yardanico, Zachary, Krux).
I probably would have struggled a lot more without the guidance of Andrea's code for Cuda in his [neo](https://github.com/unicredit/neo) and [nimcuda](https://github.com/unicredit/nimcuda) library. And obviously Araq and Dom for Nim which is an amazing language for performance, productivity, safety and metaprogramming.


Minor revisions v0.1.1 to v0.1.3
================================

Arraymancer v0.1.0. July 12, 2017 "Magician Apprentice"
===========================================

First public release.

Include:

- converting from deep nested proc or array
- Slicing, and slice mutation
- basic linear algebra operations,
- reshaping, broadcasting, concatenating,
- universal functions
- iterators (in-place, axis, inline and closure versions)
- BLAS and BLIS support for fast linear algebra
