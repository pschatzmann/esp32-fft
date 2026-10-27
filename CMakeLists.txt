cmake_minimum_required(VERSION 3.16)

if(ESP_PLATFORM)
  # ESP-IDF component
  idf_component_register(
    SRCS "src/fft.c"
    INCLUDE_DIRS "src"
  )
else()
  # Plain CMake library
  project(esp32-fft VERSION 0.1.0 LANGUAGES C)

  add_library(esp32-fft STATIC src/fft.c)
  add_library(esp32-fft::esp32-fft ALIAS esp32-fft)
  target_include_directories(esp32-fft PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src)

  find_library(MATH_LIBRARY m)
  if(MATH_LIBRARY)
    target_link_libraries(esp32-fft PUBLIC ${MATH_LIBRARY})
  endif()
endif()
