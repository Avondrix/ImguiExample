cmake_minimum_required(VERSION 3.23)
project(ImguiExample)

set(CMAKE_CXX_STANDARD 14)

set(glfw_dir _dependencies/glfw)
include_directories(${glfw_dir}/include)

set(imgui_dir _dependencies/imgui)
include_directories(${imgui_dir} ${imgui_dir}/backends)

# glfw
find_package(glfw3 REQUIRED)
include_directories(${GLFW_INCLUDE_DIRS})
link_libraries(${GLFW_LIBRARY_DIRS})

# opengl
find_package(OpenGL REQUIRED)
include_directories(${OPENGL_INCLUDE_DIRS})

if (APPLE)
    find_library(COCOA_LIBRARY Cocoa)
    find_library(OpenGL_LIBRARY OpenGL)
    find_library(IOKIT_LIBRARY IOKit)
    find_library(COREVIDEO_LIBRARY CoreVideo)
    SET(EXTRA_LIBS ${COCOA_LIBRARY} ${OpenGL_LIBRARY} ${IOKIT_LIBRARY} ${COREVIDEO_LIBRARY} )
endif (APPLE)

add_executable(ImguiExample src/main.cpp ${imgui_dir}/imgui.cpp ${imgui_dir}/backends/imgui_impl_glfw.cpp ${imgui_dir}/backends/imgui_impl_opengl3.cpp ${imgui_dir}/imgui_draw.cpp ${imgui_dir}/imgui_demo.cpp ${imgui_dir}/imgui_tables.cpp ${imgui_dir}/imgui_widgets.cpp)
target_link_libraries(ImguiExample glfw ${EXTRA_LIBS})
