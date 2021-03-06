cmake_minimum_required (VERSION 2.0)

set (CMAKE_CXX_FLAGS "-g -std=c++0x -DBOOST_LOG_DYN_LINK")

find_package (vsomeip 2.6.0 REQUIRED)
find_package ( Boost 1.55 COMPONENTS system thread log REQUIRED)

set(
    CMAKE_RUNTIME_OUTPUT_DIRECTORY
    ${CMAKE_HOME_DIRECTORY}/bin
    )

add_definitions(
    -std=c++11
    )

include_directories(
    $ENV{OPENNI2_INCLUDE}
    )

include_directories (
	${Boost_INCLUDE_DIR}
	${VSOMEIP_INCLUDE_DIRS}
)

link_directories(
    $ENV{OPENNI2_REDIST}
    )

link_libraries(
    -lOpenNI2
    -lopencv_contrib
    -lopencv_core 
    -lopencv_highgui
    -lopencv_imgproc 
    )

add_executable(service-example ./src/service-example.cpp ./src/grabber.cpp)
target_link_libraries(service-example vsomeip ${Boost_LIBRARIES})

add_executable(client-example ./src/client-example.cpp)
target_link_libraries(client-example vsomeip ${Boost_LIBRARIES})

add_executable(async_udp_echo_server ./src/async_udp_echo_server.cpp)
target_link_libraries(async_udp_echo_server ${Boost_LIBRARIES})

add_executable(udp_client ./src/udp_client.cpp)
target_link_libraries(udp_client ${Boost_LIBRARIES})

add_executable(service-camera ./src/service-camera.cpp ./src/grabber.cpp)
target_link_libraries(service-camera vsomeip ${Boost_LIBRARIES})

add_executable(client-camera ./src/client-camera.cpp ./src/grabber.cpp)
target_link_libraries(client-camera vsomeip ${Boost_LIBRARIES})