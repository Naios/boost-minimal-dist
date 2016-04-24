cmake_minimum_required(VERSION 3.0 FATAL_ERROR)
project(boost-minimal-dist LANGUAGES C CXX)

function(PrintSourceFiles)
  file(GLOB BOOST_MODULE_LIST RELATIVE
    ${CMAKE_CURRENT_LIST_DIR}/libs
    ${CMAKE_CURRENT_LIST_DIR}/libs/*)

  list(REMOVE_ITEM BOOST_MODULE_LIST "test")

  foreach(BOOST_MODULE ${BOOST_MODULE_LIST})
    if (IS_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/libs/${BOOST_MODULE})
      file(GLOB_RECURSE LOCALE_SOURCES RELATIVE
        ${CMAKE_CURRENT_LIST_DIR}
        ${CMAKE_CURRENT_LIST_DIR}/libs/${BOOST_MODULE}/src/*.cpp)
      foreach(BOOST_SOURCE ${LOCALE_SOURCES})
        message("\${CMAKE_CURRENT_LIST_DIR}/${BOOST_SOURCE}")
      endforeach()
    endif()
  endforeach()
endfunction()

# PrintSourceFiles()

set(BOOST_SOURCES
  ${CMAKE_CURRENT_LIST_DIR}/libs/atomic/src/lockpool.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/chrono/src/chrono.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/chrono/src/process_cpu_clocks.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/chrono/src/thread_clock.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/date_time/src/gregorian/date_generators.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/date_time/src/gregorian/gregorian_types.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/date_time/src/gregorian/greg_month.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/date_time/src/gregorian/greg_weekday.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/date_time/src/posix_time/posix_time_types.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/exception/src/clone_current_exception_non_intrusive.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/filesystem/src/codecvt_error_category.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/filesystem/src/operations.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/filesystem/src/path.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/filesystem/src/path_traits.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/filesystem/src/portability.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/filesystem/src/unique_path.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/filesystem/src/utf8_codecvt_facet.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/filesystem/src/windows_file_codecvt.cpp
  # ${CMAKE_CURRENT_LIST_DIR}/libs/iostreams/src/bzip2.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/iostreams/src/file_descriptor.cpp
  # ${CMAKE_CURRENT_LIST_DIR}/libs/iostreams/src/gzip.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/iostreams/src/mapped_file.cpp
  # ${CMAKE_CURRENT_LIST_DIR}/libs/iostreams/src/zlib.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/cpp_regex_traits.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/cregex.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/c_regex_traits.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/fileiter.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/icu.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/instances.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/posix_api.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/regex.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/regex_debug.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/regex_raw_buffer.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/regex_traits_defaults.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/static_mutex.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/usinstances.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/w32_regex_traits.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/wc_regex_traits.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/wide_posix_api.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/regex/src/winstances.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/smart_ptr/src/sp_collector.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/smart_ptr/src/sp_debug_hooks.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/system/src/error_code.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/thread/src/future.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/thread/src/tss_null.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/timer/src/auto_timers_construction.cpp
  ${CMAKE_CURRENT_LIST_DIR}/libs/timer/src/cpu_timer.cpp)

if (WIN32)
  list(APPEND BOOST_SOURCES
    ${CMAKE_CURRENT_LIST_DIR}/libs/thread/src/win32/thread.cpp
    ${CMAKE_CURRENT_LIST_DIR}/libs/thread/src/win32/tss_dll.cpp
    ${CMAKE_CURRENT_LIST_DIR}/libs/thread/src/win32/tss_pe.cpp)
else()
  list(APPEND BOOST_SOURCES
    ${CMAKE_CURRENT_LIST_DIR}/libs/thread/src/pthread/once.cpp
    ${CMAKE_CURRENT_LIST_DIR}/libs/thread/src/pthread/once_atomic.cpp
    ${CMAKE_CURRENT_LIST_DIR}/libs/thread/src/pthread/thread.cpp)
endif()

add_library(boost-minimal-dist STATIC ${BOOST_SOURCES})

target_include_directories(boost-minimal-dist
  PUBLIC
    ${CMAKE_CURRENT_LIST_DIR})

target_compile_features(boost-minimal-dist
  PUBLIC
    cxx_auto_type
    cxx_decltype
    cxx_final
    cxx_lambdas
    cxx_nullptr
    cxx_override)
