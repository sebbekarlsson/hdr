cmake_minimum_required(VERSION 3.20)

project(hdr)

add_compile_options(-g -Wall)

file(GLOB sources ${CMAKE_CURRENT_SOURCE_DIR}/src/*.c)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

add_executable(hdr ${sources})

file(COPY ${CMAKE_CURRENT_SOURCE_DIR}/shards DESTINATION ${CMAKE_CURRENT_BINARY_DIR})

target_include_directories(
  hdr
    PUBLIC
      $<INSTALL_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
      $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}/include>
      $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
      ${CMAKE_CURRENT_BINARY_DIR}/include
      ${CMAKE_CURRENT_SOURCE_DIR}/include)


install(TARGETS hdr
        EXPORT hdr_targets
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        RUNTIME DESTINATION bin
        INCLUDES DESTINATION include
        )
