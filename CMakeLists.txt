cmake_minimum_required(VERSION 3.17)
project(gtest_cmake_auto_dwld)

include(FetchContent)
include(CTest)

FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/master.zip
)

FetchContent_MakeAvailable(googletest)

# Now simply link against gtest or gtest_main as needed.
add_executable(example example.cpp)
target_link_libraries(example 
	gtest_main 
	gmock 
)

add_test(NAME example_test COMMAND example)
