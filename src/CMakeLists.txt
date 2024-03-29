find_package(yaml-cpp REQUIRED)
find_package(Threads REQUIRED)

set(library_name ${CMAKE_PROJECT_NAME})

add_library(${library_name}
    SHARED
    hardware.cpp
    joint.cpp
    hardware_joints.cpp
    hardware_communicator.cpp
    kinematics.cpp
    kinematics_utils.cpp
    config_file_parser.cpp
    dynamixel_x.cpp
    dynamixel_xm430.cpp
    dynamixel_xm540.cpp
    dynamixel_xh430.cpp
    dynamixel_xh540.cpp
    dynamixel_p.cpp
    dynamixel_ph42.cpp
)
set_target_properties(${library_name} PROPERTIES VERSION 1.1.0 SOVERSION 1)

target_include_directories(${library_name} PUBLIC
    ${PROJECT_SOURCE_DIR}/include
)
message("${CMAKE_THREAD_LIBS_INIT}")
target_link_libraries(${library_name} PUBLIC
    ${YAML_CPP_LIBRARIES}
    ${CMAKE_THREAD_LIBS_INIT}
    dxl_x64_cpp
)

install(TARGETS ${library_name}
    EXPORT ${library_name}-export
    LIBRARY DESTINATION lib
    INCLUDES DESTINATION include
    PUBLIC_HEADER DESTINATION include/${library_name}
)

install(DIRECTORY ${PROJECT_SOURCE_DIR}/include/
    DESTINATION include/${CMAKE_PROJECT_NAME})
