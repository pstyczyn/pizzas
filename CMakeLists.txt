cmake_minimum_required(Version 3.10)
project(Pizzas)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/03597a01ee50ed33e9dfd640b249b4be3799d395.zip
)
set(FLAGS -Wall -Wextra -Werror -pedantic -Wconversion -03)

set(SRC_LIST test/PizzeriaTest.cpp test/test_main.cpp src/Funghi.cpp src/Margherita.cpp src/Pizza.cpp src/Pizza.cpp)

add_library(${PROJECT_NAME}-lib STATIC ${SRC_LIST})
target_compile_options(${PROJECT_NAME}-lib PRIVATE ${FLAGS})


add_executable(${PROJECT_NAME} main.cpp)
target_compile_options(${PROJECT_NAME} PRIVATE ${FLAGS})
target_link_libraries(${PROJECT_NAME} ${PROJECT_NAME}-lib)
target_link_libraries(${PROJECT_NAME} pthread)


enable_testing()
add_executable(tests test/PizzeriaTest.cpp test/test_main.cpp)
add_test(NAME tests COMMAND tests)
target_compile_options(tests PRIVATE ${FLAGS})
target_link_libraries(tests test/PizzeriaTest GTest:gtest_main)
include(GoogleTest)
gtest_discover_tests(test/PizzeriaTest.cpp)
