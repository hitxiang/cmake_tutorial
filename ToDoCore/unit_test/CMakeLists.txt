set(GMOCK_DIR "$ENV{GMOCK_HOME}"
    CACHE PATH "The path to the GoogleMock test framework.")

if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "MSVC")
    # force this option to ON so that Google Test will use /MD instead of /MT
    # /MD is now the default for Visual Studio, so it should be our default, too
    option(gtest_force_shared_crt
           "Use shared (DLL) run-time lib even when Google Test is built as static lib."
           ON)
endif()
set(GMOCK_DIR ${CMAKE_SOURCE_DIR}/gmock-1.7.0)
add_subdirectory(${GMOCK_DIR} ${GMOCK_DIR}/_build)
set_property(TARGET gtest APPEND_STRING PROPERTY COMPILE_FLAGS " -w")

include_directories(SYSTEM ${GMOCK_DIR}/gtest/include
                           ${GMOCK_DIR}/include)


add_executable(ToDoTest ToDoTest.cc)
target_link_libraries(ToDoTest toDoCore
                               gmock_main)

add_test(ToDoTest ToDoTest)
