cmake_minimum_required(VERSION 3.19)

project(SDL LANGUAGES C CXX)

add_library(SDL)
add_library(SDLmain STATIC)

target_sources(SDL PRIVATE
    src/audio/disk/SDL_diskaudio.c
    src/audio/dummy/SDL_dummyaudio.c
    src/audio/SDL_audio.c
    src/audio/SDL_audiocvt.c
    src/audio/SDL_mixer.c
    src/audio/SDL_mixer_MMX_VC.c
    src/audio/SDL_wave.c
    src/audio/windib/SDL_dibaudio.c
    src/audio/windx5/SDL_dx5audio.c
    src/cdrom/SDL_cdrom.c
    src/cdrom/win32/SDL_syscdrom.c
    src/cpuinfo/SDL_cpuinfo.c
    src/events/SDL_active.c
    src/events/SDL_events.c
    src/events/SDL_expose.c
    src/events/SDL_keyboard.c
    src/events/SDL_mouse.c
    src/events/SDL_quit.c
    src/events/SDL_resize.c
    src/file/SDL_rwops.c
    src/joystick/SDL_joystick.c
    src/joystick/win32/SDL_mmjoystick.c
    src/loadso/win32/SDL_sysloadso.c
    src/SDL.c
    src/SDL_error.c
    src/SDL_fatal.c
    src/stdlib/SDL_getenv.c
    src/stdlib/SDL_iconv.c
    src/stdlib/SDL_malloc.c
    src/stdlib/SDL_qsort.c
    src/stdlib/SDL_stdlib.c
    src/stdlib/SDL_string.c
    src/thread/generic/SDL_syscond.c
    src/thread/SDL_thread.c
    src/thread/win32/SDL_sysmutex.c
    src/thread/win32/SDL_syssem.c
    src/thread/win32/SDL_systhread.c
    src/timer/SDL_timer.c
    src/timer/win32/SDL_systimer.c
    src/video/dummy/SDL_nullevents.c
    src/video/dummy/SDL_nullmouse.c
    src/video/dummy/SDL_nullvideo.c
    src/video/SDL_blit.c
    src/video/SDL_blit_0.c
    src/video/SDL_blit_1.c
    src/video/SDL_blit_A.c
    src/video/SDL_blit_N.c
    src/video/SDL_bmp.c
    src/video/SDL_cursor.c
    src/video/SDL_gamma.c
    src/video/SDL_pixels.c
    src/video/SDL_RLEaccel.c
    src/video/SDL_stretch.c
    src/video/SDL_surface.c
    src/video/SDL_video.c
    src/video/SDL_yuv.c
    src/video/SDL_yuv_sw.c
    src/video/wincommon/SDL_sysevents.c
    src/video/wincommon/SDL_sysmouse.c
    src/video/wincommon/SDL_syswm.c
    src/video/wincommon/SDL_wingl.c
    src/video/windib/SDL_dibevents.c
    src/video/windib/SDL_dibvideo.c
    src/video/Windx5/SDL_dx5events.c
    src/video/Windx5/SDL_dx5video.c
    src/video/windx5/SDL_dx5yuv.c
)

target_sources(SDLmain PRIVATE
    src/main/win32/SDL_win32_main.c
)

target_include_directories(SDL PRIVATE include)
target_include_directories(SDLmain PRIVATE include)

if (WIN32)
    target_compile_definitions(SDL PRIVATE _CRT_SECURE_NO_DEPRECATE WINDOWS_IGNORE_PACKING_MISMATCH)
    target_compile_definitions(SDLmain PRIVATE _CRT_SECURE_NO_DEPRECATE WINDOWS_IGNORE_PACKING_MISMATCH)
endif()

target_link_libraries(SDL PUBLIC winmm.lib dxguid.lib)
target_link_libraries(SDLmain PUBLIC SDL)

#target_include_directories(7zip
#    INTERFACE
#        $<INSTALL_INTERFACE:include>/7zip/CPP
#        $<INSTALL_INTERFACE:include>/7zip/C
#)

install(
    TARGETS SDL SDLmain
    EXPORT SDL-targets
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION bin
)

# Headers makes relative includes so directory structure must be kept

file(GLOB HEADERS "${CMAKE_CURRENT_LIST_DIR}/include/*.h")
install(FILES ${HEADERS} DESTINATION "include/SDL")

#include(CMakePackageConfigHelpers)
#configure_package_config_file(
#  "${CMAKE_CURRENT_SOURCE_DIR}/SDL-config.cmake.in"
#  "${CMAKE_CURRENT_BINARY_DIR}/SDL-config.cmake"
#  INSTALL_DESTINATION "share/7zip"
#)
#install(
#  FILES "${CMAKE_CURRENT_BINARY_DIR}/7zip-config.cmake"
#  DESTINATION "share/7zip"
#)

#install(
#    EXPORT 7zip-targets
#    DESTINATION share/7zip
#    NAMESPACE 7zip::
#)
