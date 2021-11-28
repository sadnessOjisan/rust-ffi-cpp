cmake_minimum_required(VERSION 3.10)
project("cmake example for Rust" LANGUAGES CXX C)

set(CMAKE_CXX_STANDARD 17)

find_package(PkgConfig)
pkg_check_modules(EGL REQUIRED egl)
pkg_check_modules(GLES2 REQUIRED glesv2)
pkg_check_modules(X11 REQUIRED x11)

set(TARGET ffi-cpp)

# 必ずstaticライブラリにビルドすること
add_library(${TARGET}
        STATIC
        example.cpp
        )

target_link_libraries(${TARGET}
        PRIVATE
        ${EGL_LIBRARIES}
        ${GLES2_LIBRARIES}
        ${X11_LIBRARIES}
        )

target_include_directories(${TARGET}
        PRIVATE
        ${EGL_INCLUDE_DIR}
        ${GLES2_INCLUDE_DIR}
        ${X11_INCLUDE_DIR}
        .
        )

# 必ずこれが必要です
install (TARGETS ${TARGET} DESTINATION .)