cmake_minimum_required(VERSION 3.16)
project(legacy-notepad LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(MSVC)
    add_compile_options(/W4 /WX /permissive- /utf-8)
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} /SUBSYSTEM:WINDOWS /ENTRY:wWinMainCRTStartup")
else()
    add_compile_options(-Wall -Wextra -Werror -municode)
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -mwindows")
endif()

add_executable(legacy-notepad WIN32
    src/main.cpp
    src/notepad.rc
)

target_link_libraries(legacy-notepad PRIVATE
    comctl32
    shlwapi
    comdlg32
)

if(NOT MSVC)
    target_link_libraries(legacy-notepad PRIVATE -static-libgcc -static-libstdc++)
endif()
