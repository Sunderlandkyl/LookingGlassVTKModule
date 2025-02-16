# Looking Glass Device Support

## Introduction

This module contains support for rendering into looking glass devices using
two main approaches. You can create a OS specific Looking Glass render
window and use it as you would a regular vtkRenderWindow. For an example of
this approach please see the TestDragon test in Testing/Cxx/TestDragon.cxx
The other approach is to use the vtkLookingGlassPass as you would normally
use a render pass in a renderer. For an example of that approach please see
Testing\Cxx\TestLookingGlassPass.cxx

## Build Requirements

Building this modules requires the Looking Glass Factory's
`HoloPlayCoreSDK`. You must request a copy of the HoloPlayCoreSDK
directly from Looking Glass Factory.

The SDK is described
[here](https://docs.lookingglassfactory.com/holoplay-core/holoplay-core-sdk).

You can request access to their SDK
[here](https://lookingglassfactory.com/software#holoplay-core).

Access is granted nearly instantaneously.  Their SDK includes dylibs
(shared libraries) for MacOS, Linux, and Windows (32 and 64bit).

We recommend installing their SDK at the same level as the
VTK source directory, so that it can be automatically found by VTK during
compilation.  For example, if VTK souce is in `/src/VTK` on your system,
then uncompress the HoloPlaceCoreSDK (which is currently at version 0.2.0) into
the `/src` directory.   The path to the HoloPlayCoreSDK include directory
would then be `/src/HoloPlayCore-0.2.0/HoloPlayCoreSDK-master/HoloPlayCore/include`.
VTK can then automatically find the include and appropriate dylib files
during CMake configuration of VTK,  otherwise you will have to specify
the paths to those files manually during CMake configuration.

## CMake Configuration of VTK

When configuring VTK using CMake, enable this remote module and its dependencies by setting
1. VTK_MODULE_ENABLE_VTK_RenderingLookingGlass to YES
2. VTK_USE_VIDEO_FOR_WINDOWS to ON
3. VTK_USE_MICROSOFT_MEDIA_FOUNDATION to ON

You must also specify
1. HoloPlayCore_INCLUDE_DIR
2. HoloPlayCore_LIBRARY

based on where you have installed the HoloPlayCore SDK, if they are not
automatically found.

## Compilation

With this module enabled in CMake, build VTK as usual for your platform. We
currently support Windows, OSX, and Linux platforms.

## Running VTK applications

Since the HoloPlayCoreSDK is distribued as shared libraries, their location
must be known when executing a VTK-based application if that version of
VTK was compiled with this module enabled.

We recommend adding the path to the appropriate shared lib to your system's
PATH/LD_LIBRARY_PATH variables.  They will then be automatically found
when running VTK applications that were compiled with this module enabled.

System-level access to the shared libs is also required when running the
Python wrapped VTK if this module was enabled when it was compiled.

## Rendering to a display and generating Quilts

The key functionality of this module is held in the `vtkLookingGlassInterface`
class.  It is used by the render window classes and by the render pass
implementations. In theory, this module should be able to generate and
display quilt images even if no Looking Glass hardware is present, but
those capabilities has not been extensively tested.

## Developement/Bug Reports

If you run into issues with this module please submit a bug report at
https://github.com/Kitware/LookingGlassVTKModule/issues

## License

See LICENSE file.
