![DirectX Logo](https://github.com/Microsoft/DirectXTK12/wiki/X_jpg.jpg)

# DirectX Tool Kit for DirectX 12

http://go.microsoft.com/fwlink/?LinkID=615561

Copyright (c) Microsoft Corporation. All rights reserved.

**December 17, 2019**

This package contains the "DirectX Tool Kit", a collection of helper classes for writing Direct3D 12 C++ code for Universal Windows Platform (UWP) apps, Win32 desktop applications for Windows 10, and Xbox One.

This code is designed to build with Visual Studio 2017 ([15.9](https://walbourn.github.io/vs-2017-15-9-update/)), Visual Studio 2019, or clang for Windows v9. It is recommended that you make use of the Windows 10 May 2019 Update SDK ([18362](https://walbourn.github.io/windows-10-may-2019-update/)).

These components are designed to work without requiring any content from the legacy DirectX SDK. For details, see [Where is the DirectX SDK?](https://aka.ms/dxsdk).

## Directory Layout

* ``Inc\``

  + Public Header Files (in the DirectX C++ namespace):

    * Audio.h - low-level audio API using XAudio2 (DirectXTK for Audio public header)
    * CommonStates.h - common D3D state combinations
    * DDSTextureLoader.h - light-weight DDS file texture loader
    * DescriptorHeap.h - helper for managing DX12 descriptor heaps
    * DirectXHelpers.h - misc C++ helpers for D3D programming
    * EffectPipelineStateDescription.h - helper for creating PSOs
    * Effects.h - set of built-in shaders for common rendering tasks
    * GamePad.h - gamepad controller helper using XInput
    * GeometricPrimitive.h - draws basic shapes such as cubes and spheres
    * GraphicsMemory.h - helper for managing dynamic graphics memory allocation
    * Keyboard.h - keyboard state tracking helper
    * Model.h - draws meshes loaded from .SDKMESH or .VBO files
    * Mouse.h - mouse helper
    * PostProcess.h - set of built-in shaders for common post-processing operations
    * PrimitiveBatch.h - simple and efficient way to draw user primitives
    * RenderTargetState.h - helper for communicating render target requirements when creating PSOs
    * ResourceUploadBatch.h - helper for managing texture resource upload to the GPU
    * ScreenGrab.h - light-weight screen shot saver
    * SimpleMath.h - simplified C++ wrapper for DirectXMath
    * SpriteBatch.h - simple & efficient 2D sprite rendering
    * SpriteFont.h - bitmap based text rendering
    * VertexTypes.h - structures for commonly used vertex data formats
    * WICTextureLoader.h - WIC-based image file texture loader
    * XboxDDSTextureLoader.h - Xbox One exclusive apps variant of DDSTextureLoader

* ``Src\``

  + DirectXTK source files and internal implementation headers

* ``Audio\``

  + DirectXTK for Audio source files and internal implementation headers

> MakeSpriteFont and XWBTool can be found in the [DirectX Tool Kit for DirectX 11](https://github.com/microsoft/DirectXTK)

# Documentation

Documentation is available on the [GitHub wiki](https://github.com/Microsoft/DirectXTK12/wiki).

## Notices

All content and source code for this package are subject to the terms of the [MIT License](http://opensource.org/licenses/MIT).

For the latest version of DirectXTK12, bug reports, etc. please visit the project site on [GitHub](https://github.com/microsoft/DirectXTK12).

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

## Xbox One

Developers using the Xbox One XDK need to generate the ``Src\Shaders\Compiled\XboxOne*.inc`` files to build the library as they are not included in the distribution package. They are built by running the script in ``Src\Shaders`` - ``CompileShaders xbox`` from the *Xbox One XDK Developer Command Prompt*. They are XDK version-specific. While they will continue to work if outdated, a mismatch will cause runtime compilation overhead that would otherwise be avoided.

## Comparisons to DirectX 11 Version

* No support for loading .CMO models or DGSL effect shaders (i.e. DGSLEffect)

* VertexTypes does not include VertexPositionNormalTangentColorTexture or VertexPositionNormalTangentColorTextureSkinning which were intended for use with the DGSL pipeline.

* DirectX Tool Kit for DirectX 11 supports Feature Level 9.x, while DirectX 12 requires Direct3D Feature Level 11.0. There are no expected DirectX 12 drivers for any lower feature level devices.

* The library assumes it is building for Windows 10 (aka ``_WIN32_WINNT=0x0A00``) so it makes use of XAudio 2.9 and WIC2 as well as DirectX 12.

* DirectX Tool Kit for Audio, GamePad, Keyboard, Mouse, and SimpleMath are identical to the DirectX 11 version.

## Release Notes

* The VS 2017/2019 projects make use of ``/permissive-`` for improved C++ standard conformance. Use of a Windows 10 SDK prior to the Fall Creators Update (16299) or an Xbox One XDK prior to June 2017 QFE 4 may result in failures due to problems with the system headers. You can work around these by disabling this switch in the project files which is found in the ``<ConformanceMode>`` elements, or in some cases adding ``/Zc:twoPhase-`` to the ``<AdditionalOptions>`` elements.

* The VS 2017 projects require the 15.5 update or later. For UWP and Win32 classic desktop projects with the 15.5 - 15.7 updates, you need to install the standalone Windows 10 SDK (17763) which is otherwise included in the 15.8.6 or later update. Older VS 2017 updates will fail to load the projects due to use of the <ConformanceMode> element. If using the 15.5 or 15.6 updates, you will see ``warning D9002: ignoring unknown option '/Zc:__cplusplus'`` because this switch isn't supported until 15.7. It is safe to ignore this warning, or you can edit the project files ``<AdditionalOptions>`` elements.

* The VS 2019 projects use a ``<WindowsTargetPlatformVersion>`` of ``10.0`` which indicates to use the latest installed version. This should be Windows 10 SDK (17763) or later.

* The UWP projects and the VS 2019 Win10 classic desktop project include configurations for the ARM64 platform. These require VS 2017 (15.9 update) or VS 2019 to build, with the ARM64 toolset installed.

* The CompileShaders.cmd script must have Windows-style (CRLF) line-endings. If it is changed to Linux-style (LF) line-endings, it can fail to build all the required shaders.

