autocrop
========

This package contains a tool for automatically cropping and deskewing
images of book pages captured by an Internet Archive Scribe bookscanner.

This software was written as a side project in 2008 and has not been
optimized. In its current state, it can process a single page image in
about 2 seconds on a Scribe bookscanner. Since it is too slow to run in
realtime during the scanning process, it was never deployed.
(Update: it was deployed in 2011)

## Installation

To compile autocrop scribe simply run:

    $ make

To run tests, compile with `make CXXFLAGS=-DWRITE_DEBUG_IMAGES`

Here is a walkthrough for building, downloading test data, and running tests:

    # install dependencies
    $ sudo apt-get install libjpeg-dev libpng-dev libtiff-dev

    # clone and build
    $ git clone git@github.com:rajbot/autocrop.git
    $ cd autocrop/
    $ make CXXFLAGS=-DWRITE_DEBUG_IMAGES

    # download test images and run tests
    $ cd tests/
    $ wget http://archive.org/download/autocrop_test_data/autocrop_test_data_images.zip
    $ unzip autocrop_test_data_images.zip
    $ mv autocrop_test_data_images testimg
    $ wget http://archive.org/download/autocrop_test_data/testimg_foldout.zip
    $ unzip testimg_foldout.zip
    $ make test

## Project Structure

*autoCropFoldout.c* contains code that crops to the edges of a page shot
against a black background. If you are investigating this project for
your own scanning, autoCropFoldout would probably be the best place to
start.

Example output of autoCropFoldout is available here:
http://archive.org/download/autocrop_test_data/foldout_test.zip/foldout_test%2Findex.html

*autoCropScibe.c* contains the autocrop code for the Scribe bookscanner.

Example output of the autocrop algorithm is available here:
http://www.archive.org/download/autocrop_test_picturesquenewen00swee/picturesquenewen00swee/index.html

*processScribe.py* is a wrapper that will process images after the image
capture phase is complete and will write crop and skew information into
scandata.xml (which is created by Scribe).

*autoCropScribe* depends on the Leptonica image processing library. This
tool has been compiled against Leptonica 1.56 and has not been tested
with more modern versions of Leptionica.
(Update: now compiled with Leptonica 1.68)