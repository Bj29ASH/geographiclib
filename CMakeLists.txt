cmake_minimum_required(VERSION 3.27)
project(geographiclib VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(geographiclib INTERFACE)

target_link_directories(geographiclib
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/lib>
  $<INSTALL_INTERFACE:lib/geographiclib>
)

target_include_directories(geographiclib
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include/geographiclib>
)

target_link_libraries(geographiclib
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/lib/Geographic.lib>
  $<INSTALL_INTERFACE:Geographic.lib>
)

include(CMakePackageConfigHelpers)
configure_package_config_file(
  "${CMAKE_CURRENT_SOURCE_DIR}/geographiclibConfig.cmake.in"
  "${CMAKE_CURRENT_BINARY_DIR}/geographiclibConfig.cmake"
  INSTALL_DESTINATION share/geographiclib
)

install(TARGETS geographiclib
  EXPORT geographiclibTargets
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

install(DIRECTORY
  "${CMAKE_CURRENT_SOURCE_DIR}/include/GeographicLib"
  DESTINATION include/geographiclib
)

install(FILES
  "${CMAKE_CURRENT_SOURCE_DIR}/lib/Geographic.lib"
  DESTINATION lib/geographiclib
)

install(
  EXPORT geographiclibTargets
  DESTINATION share/geographiclib
  NAMESPACE geographiclib::
)

install(
  FILES
  "${CMAKE_CURRENT_BINARY_DIR}/geographiclibConfig.cmake"
  DESTINATION share/geographiclib
)
