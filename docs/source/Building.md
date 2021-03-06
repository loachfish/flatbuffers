Building    {#flatbuffers_guide_building}
========

## Building with Visual Studio or Xcode projects

There are project files for Visual Studio and Xcode that should allow you
to build the compiler `flatc`, the samples and the tests out of the box.

## Building with CMake

Alternatively, the distribution comes with a `cmake` file that should allow
you to build project/make files for any platform. For details on `cmake`, see
<http://www.cmake.org>. In brief, depending on your platform, use one of
e.g.:

    cmake -G "Unix Makefiles"
    cmake -G "Visual Studio 10"
    cmake -G "Xcode"

Then, build as normal for your platform. This should result in a `flatc`
executable, essential for the next steps.
Note that to use clang instead of gcc, you may need to set up your environment
variables, e.g.
`CC=/usr/bin/clang CXX=/usr/bin/clang++ cmake -G "Unix Makefiles"`.

Optionally, run the `flattests` executable from the root `flatbuffers/`
directory to ensure everything is working correctly on your system. If this
fails, please contact us!

Building should also produce two sample executables, `flatsamplebinary` and
`flatsampletext`, see the corresponding `.cpp` files in the
`flatbuffers/samples` directory.

*Note that you MUST be in the root of the FlatBuffers distribution when you
run 'flattests' or `flatsampletext`, or it will fail to load its files.*

## Building for Android

There is a `flatbuffers/android` directory that contains all you need to build
the test executable on android (use the included `build_apk.sh` script, or use
`ndk_build` / `adb` etc. as usual). Upon running, it will output to the log
if tests succeeded or not.

You may also run an android sample from inside the `flatbuffers/samples`, by
running the `android_sample.sh` script. Optionally, you may go to the
`flatbuffers/samples/android` folder and build the sample with the
`build_apk.sh` script or `ndk_build` / `adb` etc.

## Using FlatBuffers in your own projects.

For C++, there is usually no runtime to compile, as the code consists of a
single header, `include/flatbuffers/flatbuffers.h`. You should add the
`include` folder to your include paths. If you wish to be
able to load schemas and/or parse text into binary buffers at runtime,
you additionally need the other headers in `include/flatbuffers`. You must
also compile/link `src/idl_parser.cpp` (and `src/idl_gen_text.cpp` if you
also want to be able convert binary to text).

To see how to include FlatBuffers in any of our supported languages, please
view the [Tutorial](@ref flatbuffers_guide_tutorial) and select your appropriate
language using the radio buttons.

#### For Google Play apps

For applications on Google Play that integrate this library, usage is tracked.
This tracking is done automatically using the embedded version string
(flatbuffer_version_string), and helps us continue to optimize it.
Aside from consuming a few extra bytes in your application binary, it shouldn't
affect your application at all. We use this information to let us know if
FlatBuffers is useful and if we should continue to invest in it. Since this is
open source, you are free to remove the version string but we would appreciate
if you would leave it in.
