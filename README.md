# ![DCV](http://ljubobratovicrelja.github.io/dcv/images/dcv_logo.png)

[![Build Status](https://travis-ci.org/ljubobratovicrelja/dcv.svg?branch=master)](https://travis-ci.org/ljubobratovicrelja/dcv) [![codecov.io](https://codecov.io/github/ljubobratovicrelja/dcv/coverage.svg?branch=master)](https://codecov.io/github/ljubobratovicrelja/dcv?branch=master) [![Join the chat at https://gitter.im/ljubobratovicrelja/dcv](https://badges.gitter.im/ljubobratovicrelja/dcv.svg)](https://gitter.im/ljubobratovicrelja/dcv?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge) [![DUB](https://img.shields.io/dub/v/dcv.svg)](http://code.dlang.org/packages/dcv) [![DUB](https://img.shields.io/dub/dt/dcv.svg)](http://code.dlang.org/packages/dcv)

*Computer Vision Library for D Programming Language*

## About

DCV is an open source computer vision library, written in D programming language, with goal to provide tools for solving most common computer vision problems - various image processing tasks, feature detection and tracking, camera calibration, stereo etc.

## Focus

Focus of the library is to present an easy-to-use interface, that would attract computer vision scientists and engineers to prototype their solutions with, but also to provide fast running code that could be used to make production ready tools and applications.

## API

DCV's API heavily utilizes [std.experimental.ndslice](https://dlang.org/phobos/std_experimental_ndslice.html) package, which originated in [Mir](https://github.com/libmir/mir) project. It's n-dimensional range view structure [Slice](https://dlang.org/phobos/std_experimental_ndslice_slice.html#.Slice) is used for any form of image manipulation and processing. But overall shape of the API is adopted from well known computer vision toolkits such as Matlab Image Processing Toolbox, and OpenCV library, to be easily familiarized with. But it's also spiced up with D's syntactic sugar, to support pipelined calls:

```d
Image image = imread("/path/to/image.png"); // read an image from filesystem.

auto slice = image.sliced; // slice image data (calls std.experimental.ndslice.slice.sliced on image data)

slice
    .asType!float[0..$, 0..$, 1] // convert slice data to float, and take the green channel only.
    .conv!symmetric(sobel!float(GradientDirection.DIR_X)) // convolve image with horizontal Sobel kernel.
    .byElement
    .ranged(0, 255).array.sliced(slice.shape[0..2]) // scale values to fit the range between the 0 and 255
    .imshow("Sobel derivatives"); // preview changes on screen.

waitKey();
```

## Documentation

API reference, and examples can be found in project gh-pages: [https://ljubobratovicrelja.github.io/dcv/](https://ljubobratovicrelja.github.io/dcv/). Also project roadmap, news and other related stuff should be always located on the site's home page.

## Contributions
PRs and any form of help is most appreciated. Also, you can file an issue for feature request, bug report or any other library related inquiry. If you have any sort of quick question, feel free to post it in the gitter room.

## License
Library is licensed under Boost Software License - Version 1.0. Some modules in the library contain code that is licensed under some other terms. If a module in the library states different license terms in it's header, then the Boost Software License does not apply to that module.

