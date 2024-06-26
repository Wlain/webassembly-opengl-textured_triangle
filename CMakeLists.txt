cmake_minimum_required(VERSION 3.10)
project(textureDemo)


# Add the source file
add_executable(textureDemo main.cpp)

add_definitions(-DRESOURCES_DIR="${CMAKE_CURRENT_SOURCE_DIR}/assets")
# Set compile options
set_target_properties(textureDemo PROPERTIES
        LINK_FLAGS "-s USE_WEBGL2=1 --preload-file ${CMAKE_CURRENT_SOURCE_DIR}/assets --use-preload-plugins -o ${CMAKE_CURRENT_LIST_DIR}/index.js"
)

add_custom_command(
        TARGET textureDemo POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy
        ${CMAKE_SOURCE_DIR}/index.html $<TARGET_FILE_DIR:textureDemo>/index.html
)