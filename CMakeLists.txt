cmake_minimum_required(Version 3.10)
project(Pizzas)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(FLAGS -Wall -Wextra -Werror -pedantic -Wconversion -03)

set(SRC_LIST test/PizzeriaTest.cpp test/test_main.cpp src/Funghi.cpp src/Margherita.cpp src/Pizza.cpp src/Pizza.cpp)

add_library(${PROJECT_NAME}-lib STATIC ${SRC_LIST})
target_compile_options(${PROJECT_NAME}-lib PRIVATE ${FLAGS})


add_executable(${PROJECT_NAME} main.cpp)
target_compile_options(${PROJECT_NAME} PRIVATE ${FLAGS})
target_link_libraries(${PROJECT_NAME} ${PROJECT_NAME}-lib)
target_link_libraries(${PROJECT_NAME} pthread)
