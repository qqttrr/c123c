cmake_minimum_required(VERSION 2.8)
set(CMAKE_CXX_STANDARD 11)
project(test)
if (NOT TARGET ServerLibrary)
    add_subdirectory("../lib" "${CMAKE_CURRENT_BINARY_DIR}/lib_build")
endif ()
enable_testing()
include_directories(${LIBHIREDIS_INCLUDE_DIR})
include_directories(${LIBEVENT_INCLUDE_DIR})
include_directories(${evhtp_INCLUDE_DIR})
set(LIBS ${LIBS} ${evhtp_LIBRARIES})
set(LIBS ${LIBS} ${LIBHIREDIS_LIBRARIES})
set(LIBS ${LIBS} ${LIBEVENT_LIB})
include_directories(${gtest_SOURCE_DIR}/include ${gtest_SOURCE_DIR})
add_executable(UnitTests tests.cpp)
target_link_libraries(UnitTests ${CMAKE_CURRENT_SOURCE_DIR}/gtestbuild/libgtest_main.a ${CMAKE_CURRENT_SOURCE_DIR}/gtestbuild/libgtest.a
        ${LIBS}
        ServerLibrary)

add_test(UnitTests UnitTests)
