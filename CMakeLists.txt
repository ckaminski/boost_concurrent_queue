cmake_minimum_required(VERSION 3.0)
#set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/Modules)

# boost
find_package(Boost 1.50.0 REQUIRED system thread )
include_directories(${Boost_INCLUDE_DIRS})
link_directories(${Boost_LIBRARY_DIRS})

add_subdirectory(libs/catch libs/catch)
add_library(Catch INTERFACE)
target_include_directories(Catch INTERFACE ${PROJECT_SOURCE_DIR}/libs/catch/include)


# TODO: test for C++ or better

set(CMAKE_CXX_FLAGS "-std=c++11 -pedantic")
#g++ -std=c++11 -pedantic

include_directories(include ${PROJECT_SOURCE_DIR}/libs/catch)

link_libraries(
    ${Boost_LIBRARIES}
)

add_executable(test1
    test/test1.cpp
)
target_link_libraries(test1 Catch ${Boost_LIBRARIES})
target_include_directories(test1 PUBLIC 
                                 ${PROJECT_SOURCE_DIR}/include 
                                 ${PROJECT_SOURCE_DIR}/libs/catch/include)

enable_testing()
add_test(NAME test1 COMMAND test1)
