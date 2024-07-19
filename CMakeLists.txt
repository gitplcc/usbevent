cmake_minimum_required(VERSION 3.16...3.28)

project(
    usbevent
    VERSION 0.0.1
    DESCRIPTION "Check libusb event capability"
    LANGUAGES C CXX
)

#~ include(CheckIncludeFile)
include(CheckIPOSupported)
#~ include(CheckPIESupported)
#~ include(CheckSymbolExists)
#~ include(CheckTypeSize)
include(CMakeDependentOption)
#~ include(CMakePackageConfigHelpers)
#~ include(GNUInstallDirs)

find_program(CCACHE_PROGRAM ccache)
cmake_dependent_option(CCACHE_ENABLED
  "Use ccache to speed-up build." ON
  "CCACHE_PROGRAM" OFF
)
if(CCACHE_ENABLED)
  set(CMAKE_C_COMPILER_LAUNCHER "${CCACHE_PROGRAM}")
endif()

find_package(PkgConfig REQUIRED)

pkg_check_modules(LIBUSB1 REQUIRED IMPORTED_TARGET libusb-1.0>=1.0.16)
                  
check_ipo_supported(RESULT IPO_SUPPORTED LANGUAGES C CXX)
#~ check_pie_supported(OUTPUT_VARIABLE PIE_SUPPORTED LANGUAGES C CXX)

#~ configure_file(config.h.cmake config.h)

add_subdirectory(libtdms)
add_subdirectory(usbevent)
