# SPDX-License-Identifier: Apache-2.0 WITH LLVM-exception

add_library(beman.exemplar STATIC)
add_library(beman::exemplar ALIAS beman.exemplar)

target_sources(beman.exemplar PRIVATE identity.cpp)

target_include_directories(
  beman.exemplar
  PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../../../include>)

install(
  TARGETS beman.exemplar
  EXPORT beman.exemplar
  DESTINATION ${CMAKE_INSTALL_LIBDIR})

install(
  DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/../../../include/
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
  FILES_MATCHING
  PATTERN "*.hpp")

if(BUILD_TESTING)
  include(GoogleTest)

  add_executable(beman.exemplar.tests)
  target_sources(beman.exemplar.tests PRIVATE identity.t.cpp)
  target_link_libraries(beman.exemplar.tests
                        PRIVATE beman::exemplar GTest::gtest GTest::gtest_main)

  gtest_add_tests(beman.exemplar.tests "" AUTO)
endif()
