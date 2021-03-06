# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.4.1)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -D__STDC_CONSTANT_MACROS")
set(CMAKE_CPP_FLAGS "${CMAKE_CPP_FLAGS} -D__STDC_CONSTANT_MACROS")

include_directories(
            ${CMAKE_SOURCE_DIR}/sharedcpp/3rdparty
            ${CMAKE_SOURCE_DIR}/sharedcpp/3rdparty/ffmpeg/include
            ${CMAKE_SOURCE_DIR}/sharedcpp/libcommon
            ${CMAKE_SOURCE_DIR}/sharedcpp/video_encoder
            ${CMAKE_SOURCE_DIR}/sharedcpp/libeditcore
            ${CMAKE_SOURCE_DIR}/sharedcpp/audio_effect
            ${CMAKE_SOURCE_DIR}/sharedcpp/video_consumer
            ${CMAKE_SOURCE_DIR}/sharedcpp/liblivecore)

add_library(
            fdk-aac
            STATIC
            IMPORTED
            )

set_target_properties(
            fdk-aac
            PROPERTIES IMPORTED_LOCATION
            ${CMAKE_SOURCE_DIR}/sharedcpp/3rdparty/prebuilt/${ANDROID_ABI}/libfdk-aac.a
            )

add_library(
            avfilter
            STATIC
            IMPORTED
            )

set_target_properties(
            avfilter
            PROPERTIES IMPORTED_LOCATION
            ${CMAKE_SOURCE_DIR}/sharedcpp/3rdparty/prebuilt/${ANDROID_ABI}/libavfilter.a
            )

add_library(
            vo-aacenc
            STATIC
            IMPORTED
            )

set_target_properties(
            vo-aacenc
            PROPERTIES IMPORTED_LOCATION
            ${CMAKE_SOURCE_DIR}/sharedcpp/3rdparty/prebuilt/${ANDROID_ABI}/libvo-aacenc.a
            )

add_library(
            avformat
            STATIC
            IMPORTED
            )

set_target_properties(
            avformat
            PROPERTIES IMPORTED_LOCATION
            ${CMAKE_SOURCE_DIR}/sharedcpp/3rdparty/prebuilt/${ANDROID_ABI}/libavformat.a
            )

add_library(
            avcodec
            STATIC
            IMPORTED
            )

set_target_properties(
            avcodec
            PROPERTIES IMPORTED_LOCATION
            ${CMAKE_SOURCE_DIR}/sharedcpp/3rdparty/prebuilt/${ANDROID_ABI}/libavcodec.a
            )

add_library(
            avutil
            STATIC
            IMPORTED
            )

set_target_properties(
            avutil
            PROPERTIES IMPORTED_LOCATION
            ${CMAKE_SOURCE_DIR}/sharedcpp/3rdparty/prebuilt/${ANDROID_ABI}/libavutil.a
            )

add_library(
            swscale
            STATIC
            IMPORTED
            )

set_target_properties(
            swscale
            PROPERTIES IMPORTED_LOCATION
            ${CMAKE_SOURCE_DIR}/sharedcpp/3rdparty/prebuilt/${ANDROID_ABI}/libswscale.a
            )

add_library(
            swresample
            STATIC
            IMPORTED
            )

set_target_properties(
            swresample
            PROPERTIES IMPORTED_LOCATION
            ${CMAKE_SOURCE_DIR}/sharedcpp/3rdparty/prebuilt/${ANDROID_ABI}/libswresample.a
            )

add_library(
            postproc
            STATIC
            IMPORTED
            )

set_target_properties(
            postproc
            PROPERTIES IMPORTED_LOCATION
            ${CMAKE_SOURCE_DIR}/sharedcpp/3rdparty/prebuilt/${ANDROID_ABI}/libpostproc.a
            )

add_library(
            x264
            STATIC
            IMPORTED
            )

set_target_properties(
            x264
            PROPERTIES IMPORTED_LOCATION
            ${CMAKE_SOURCE_DIR}/sharedcpp/3rdparty/prebuilt/${ANDROID_ABI}/libx264.a
            )

add_library(
            sox
            STATIC
            IMPORTED
            )

set_target_properties(
            sox
            PROPERTIES IMPORTED_LOCATION
            ${CMAKE_SOURCE_DIR}/sharedcpp/3rdparty/prebuilt/${ANDROID_ABI}/libsox.a
            )

add_subdirectory(${CMAKE_SOURCE_DIR}/sharedcpp/audio_effect)
add_subdirectory(${CMAKE_SOURCE_DIR}/sharedcpp/camera_preview)
add_subdirectory(${CMAKE_SOURCE_DIR}/sharedcpp/libcommon)
add_subdirectory(${CMAKE_SOURCE_DIR}/sharedcpp/libeditcore)
add_subdirectory(${CMAKE_SOURCE_DIR}/sharedcpp/liblivecore)
add_subdirectory(${CMAKE_SOURCE_DIR}/sharedcpp/music_decoder)
add_subdirectory(${CMAKE_SOURCE_DIR}/sharedcpp/recorder_processor)
add_subdirectory(${CMAKE_SOURCE_DIR}/sharedcpp/video_consumer)
add_subdirectory(${CMAKE_SOURCE_DIR}/sharedcpp/video_encoder)

# static lib
add_library(songstudio
            camera_preview/jni/ChangbaRecordingPreviewScheduler.cpp
            video_consumer/jni/VideoStudio.cpp
            recorder_processor/jni/NativeRecordProcessor.cpp
            music_decoder/jni/MusicDecoder.cpp
            )

target_link_libraries(songstudio

                libcommontool
                libaudioeffect
                libmusicdecoder
                librecordprocessor
                libcamerapreview
                libvideoencoder
                libeditcore
                liblivecore
                libvideoconsumer

                avfilter
                avformat
                avcodec
                fdk-aac
                vo-aacenc
                avutil
                swscale
                swresample
                postproc
                #sox
                x264

                GLESv2
                OpenSLES
                EGL
                z
                gomp
                android
                log
                )