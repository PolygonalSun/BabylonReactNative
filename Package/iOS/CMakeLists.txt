cmake_minimum_required(VERSION 3.13.2)
project(ReactNativeBabylon)
include(${CMAKE_CURRENT_SOURCE_DIR}/../../Apps/Playground/Playground/node_modules/@babylonjs/react-native-iosandroid/ios/CMakeLists.txt)

set(PACKAGED_LIBS
    astc-codec
    astc
    bgfx
    bimg
    bx
    Canvas
    GenericCodeGen
    glslang
    Graphics
    JsRuntime
    OGLCompiler
    OSDependent
    MachineIndependent
    napi
    NativeCapture
    NativeEngine
    NativeInput
    NativeOptimizations
    NativeTracing
    NativeXr
    SPIRV
    spirv-cross-core
    spirv-cross-glsl
    spirv-cross-msl
    tinyexr
    UrlLib
    Window
    XMLHttpRequest
    xr
)

foreach(packaged_lib ${PACKAGED_LIBS})
    add_custom_command(TARGET BabylonNative POST_BUILD
        COMMAND cp $<TARGET_FILE:${packaged_lib}> $<TARGET_FILE_DIR:BabylonNative>
        DEPENDS ${packaged_lib}
    )
endforeach()