cmake_minimum_required(VERSION 3.10 FATAL_ERROR)
project(CGBE C)

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
set(CMAKE_BUILD_TYPE Debug)

include(CheckCSourceCompiles)
include(CheckCSourceRuns)
include(CheckFunctionExists)
include(CheckIncludeFile)
include(CheckIncludeFiles)
include(CheckLibraryExists)
include(CheckSymbolExists)
include(CheckTypeSize)

set(INCLUDES "")
macro(ck_check_include_file header var)
  check_include_files("${INCLUDES};${header}" ${var})
  if(${var})
    set(INCLUDES ${INCLUDES} ${header})
  endif()
endmacro()

ck_check_include_file("stdlib.h" HAVE_STDLIB_H)
check_type_size(intmax_t INTMAX_T)
check_type_size(uintmax_t UINTMAX_T)
check_type_size(pid_t PID_T)

if(NOT HAVE_PID_T)
  if(WIN32)
    set(pid_t "int")
  else()
    message(FATAL_ERROR "pid_t doesn't exist on this platform?")
  endif()
endif()

if(WIN32)
  # Windows-specific paths...
else()
  find_package(SDL2 REQUIRED)
  find_package(SDL2_ttf REQUIRED)
  
  # Fallback if FindSDL2_ttf didn't set the libraries variable
  if(NOT SDL2_TTF_LIBRARIES)
    find_library(SDL2_TTF_LIBRARY NAMES SDL2_ttf)
    if(SDL2_TTF_LIBRARY)
      set(SDL2_TTF_LIBRARIES ${SDL2_TTF_LIBRARY})
    else()
      message(FATAL_ERROR "SDL2_ttf library not found")
    endif()
  endif()
endif()

include_directories(${SDL2_INCLUDE_DIRS} ${SDL2_TTF_INCLUDE_DIRS})

add_subdirectory(lib)
add_subdirectory(cgbe)
