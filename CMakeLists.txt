cmake_minimum_required(VERSION 3.14)
project(realsense_example)

add_subdirectory(thirdparty)
find_package(realsense2 REQUIRED CONFIG
        PATHS ${CMAKE_BINARY_DIR}/librealsense/lib/cmake/realsense2)

add_executable(realsense_example)
add_subdirectory(src)
target_link_libraries(realsense_example
        ${realsense2_LIBRARY}
)

add_custom_command(TARGET realsense_example
        POST_BUILD
        # Copy dependencies to binary folder
        COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:${realsense2_LIBRARY}> ${PROJECT_BINARY_DIR}/
        )
