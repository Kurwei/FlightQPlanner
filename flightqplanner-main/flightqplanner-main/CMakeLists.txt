cmake_minimum_required(VERSION 3.16)

project(FlightQPlanner VERSION 1.0 LANGUAGES CXX)

# C++ 17 Version
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Setting the binary directory
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/bin)

# Automatically generating QT tools
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

# Find Qt Modules (core gui widgets)
find_package(Qt6 REQUIRED COMPONENTS Core Gui Widgets)
find_package(Qt6 REQUIRED COMPONENTS Core SerialPort Widgets)

# Source, Header, Interface and QRC Files
set(PROJECT_SOURCES
    main.cpp
    mainwindow.cpp
    FController.cpp
    mainwindow.h
    FController.h
    mainwindow.ui
    resources.qrc
)

# Create executable file
add_executable(${PROJECT_NAME} ${PROJECT_SOURCES})

if(MSVC)
    add_compile_options(/W0)
else()
    add_compile_options(-Wno-error -w)
endif()

# Private definitions
target_compile_definitions(${PROJECT_NAME} PRIVATE MAVSDK_ENABLE_MAVLINK_C_API)

# Include Paths
target_include_directories(${PROJECT_NAME} PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    $ENV{DEV_EXTERNALS_PATH}/USBSDK_Thermal/include
)

# Libraries depending on Operating Systems
if(APPLE)
    # macOS - Homebrew
    target_include_directories(${PROJECT_NAME} PRIVATE
        /opt/homebrew/include
        /opt/homebrew/include/mavsdk
        /opt/homebrew/include/opencv4
    )
    target_link_directories(${PROJECT_NAME} PRIVATE /opt/homebrew/lib)
    target_link_libraries(${PROJECT_NAME} PRIVATE mavsdk)
elseif(UNIX AND NOT APPLE)
    # Linux / Ubuntu
    target_include_directories(${PROJECT_NAME} PRIVATE
        /usr/include
        /usr/include/mavsdk
        /usr/include/opencv4
        /usr/include/gazebo-11
        /usr/include/sdformat-9.7
    )
    target_link_directories(${PROJECT_NAME} PRIVATE /usr/lib)
    target_link_libraries(${PROJECT_NAME} PRIVATE mavsdk X11)

    # Install Target
    install(TARGETS ${PROJECT_NAME} DESTINATION /opt/${PROJECT_NAME}/bin)
endif()

# Bind Qt Libraries
target_link_libraries(${PROJECT_NAME} PRIVATE
    Qt6::Core
    Qt6::Gui
    Qt6::SerialPort
    Qt6::Widgets
)