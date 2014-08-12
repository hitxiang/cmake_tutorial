==== CMakeLists.txt at top ====
```
project(AAAA_test)
cmake_minimum_required(VERSION 2.6)

enable_testing()

set(GMOCK_HOME ${CMAKE_SOURCE_DIR}/gmock-1.7.0)
file(MAKE_DIRECTORY ${GMOCK_HOME}/_build)
add_subdirectory(${GMOCK_HOME} ${GMOCK_HOME}/_build)
include_directories(${GMOCK_HOME}/include ${GMOCK_HOME}/gtest/include)
#link_directories($GMOCK_HOME/_build $GMOCK_HOME/gtest/_build)

include_directories(${CMAKE_SOURCE_DIR}/include)

#add_definitions(-std=c++0x)
set(warnings "-Wall -Wextra -Werror")
set(CMAKE_CXX_FLAGS "${warnings}")
set(CMAKE_C_FLAGS   "${warnings}")

add_subdirectory(util/unit_test)
add_subdirectory(lib/unit_test)
```

==== CMakeLists.txt in util/unit_test ====
```
add_executable(UtilTest
    atl_string_test.cpp "../atl_string.c")
target_link_libraries(UtilTest gtest_main)

add_test(NAME UtilTest
         COMMAND UtilTest "--gtest_output=xml:util_report.xml")
```


==== CMakeLists.txt in lib/unit_test ====
```
add_executable(LibTest
    atl_zlib_test.cpp)
target_link_libraries(LibTest gtest_main)

add_test(NAME LibTest
         COMMAND LibTest "--gtest_output=xml:lib_report.xml")
```
