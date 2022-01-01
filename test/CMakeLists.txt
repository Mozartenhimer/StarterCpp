# find_package(Catch2 REQUIRED)
CPMAddPackage("gh:catchorg/Catch2@2.13.7")

# message(${CPM_SOURCE_CACHE})
# find_file(catch2_cmake Catch.cmake
#   HINTS ${CPM_SOURCE_CACHE})
# include(${catch2_cmake})

add_library(catch_main STATIC catch_main.cpp)
target_link_libraries(catch_main PUBLIC Catch2::Catch2)
target_link_libraries(catch_main PRIVATE project_options)

add_executable(tests tests.cpp)
target_link_libraries(tests PRIVATE project_warnings project_options catch_main)
add_test(all_tests tests)


# Doesn't work now because I can't find Catch.cmake
# automatically discover tests that are defined in catch based test files you can modify the unittests. Set TEST_PREFIX
# to whatever you want, or use different for different binaries
# catch_discover_tests(
#   tests # Create
#   TEST_PREFIX "unittests."
#   REPORTER     xml
#   OUTPUT_DIR   .
#   OUTPUT_PREFIX "unittests."
#   OUTPUT_SUFFIX  .xml)