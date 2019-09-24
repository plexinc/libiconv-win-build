cmake_minimum_required(VERSION 3.11)

project(libiconv C)

add_library(libiconv SHARED
  libcharset/lib/localcharset.c
  lib/iconv.c

  win32/libiconv.rc
)

target_compile_definitions(libiconv
  PRIVATE
    BUILDING_LIBICONV
  PUBLIC
    LIBICONV_DLL
    _CRT_SECURE_NO_WARNINGS
)

target_include_directories(libiconv PRIVATE
  include
  lib
  srclib
)

target_compile_options(libiconv PUBLIC
  -Wno-parentheses-equality
  -Wno-unused-function
)

add_executable(iconv
  srclib/progname.c
  srclib/safe-read.c
  srclib/uniwidth/width.c
  src/iconv_no_i18n.c
  win32/iconv.rc)

target_link_libraries(iconv libiconv)

target_include_directories(iconv PRIVATE
  src
  include
  srclib
  lib
)