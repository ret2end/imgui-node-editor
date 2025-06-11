cmake_minimum_required(VERSION 3.15)

project(cimguinodeeditor)

#general settings
file(GLOB IMGUI_SOURCES
    ../imgui/imgui.cpp
    ../imgui/imgui_draw.cpp
    ../imgui/imgui_demo.cpp
    ../imgui/imgui_widgets.cpp
	../imgui/imgui_tables.cpp
    imgui_node_editor.cpp
    imgui_node_editor_api.cpp
    crude_json.cpp
    imgui_canvas.cpp
)

set(IMGUI_STATIC "no" CACHE STRING "Build as a static library")
set(IMGUI_WCHAR32 "no" CACHE STRING "Build with ImWChar32")
set(CMAKE_CXX_STANDARD 14)

if (IMGUI_WCHAR32)
    add_definitions("-DIMGUI_USE_WCHAR32=1")
endif(IMGUI_WCHAR32)

#add library and link
if (IMGUI_STATIC)
    add_library(cimguinodeeditor STATIC ${IMGUI_SOURCES})
else (IMGUI_STATIC)
    add_library(cimguinodeeditor SHARED ${IMGUI_SOURCES})
endif (IMGUI_STATIC)

target_compile_definitions(cimguinodeeditor PUBLIC IMGUI_DISABLE_OBSOLETE_FUNCTIONS=1)
target_include_directories(cimguinodeeditor PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/)
target_include_directories(cimguinodeeditor PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../imgui)
set_target_properties(cimguinodeeditor PROPERTIES PREFIX "")

#install
install(TARGETS cimguinodeeditor
    RUNTIME DESTINATION  .
    LIBRARY DESTINATION  .
    ARCHIVE DESTINATION  .
)