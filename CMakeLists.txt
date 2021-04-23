cmake_minimum_required(VERSION 3.17)
project(gtest_cmake_auto_dwld)

include(FetchContent)

# https://stackoverflow.com/questions/24750215/getting-the-last-commit-hash-from-a-remote-repo-without-cloning
# https://stackoverflow.com/questions/35689501/cmakes-execute-process-and-arbitrary-shell-scripts
execute_process(
  COMMAND bash "-c" "git ls-remote https://github.com/google/googletest.git HEAD | cut -f1"
  OUTPUT_VARIABLE GIT_COMMIT_HASH
  OUTPUT_STRIP_TRAILING_WHITESPACE
)

message(STATUS "GIT_COMMIT_HASH : ${GIT_COMMIT_HASH}")

FetchContent_Declare(
  googletest
  # Specify the commit you depend on and update it regularly.
  URL https://github.com/google/googletest/archive/${GIT_COMMIT_HASH}.zip
)

FetchContent_MakeAvailable(googletest)

# Now simply link against gtest or gtest_main as needed.
add_executable(example example.cpp)
target_link_libraries(example 
	gtest_main 
	gmock 
#	pthread
)
add_test(NAME example_test COMMAND example)
