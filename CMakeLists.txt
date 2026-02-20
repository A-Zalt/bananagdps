cmake_minimum_required(VERSION 3.10)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(ANDROID_ABI armeabi-v7a)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(banana)

add_library(banana SHARED src/main.cc)

set(DOBBY_DEBUG OFF CACHE INTERNAL "" FORCE)
set(DOBBY_GENERATE_SHARED OFF CACHE INTERNAL "" FORCE)
add_definitions(-DLOGGING_DISABLE -DNDEBUG)
add_subdirectory(include/Dobby)

target_compile_options(banana PUBLIC -fdebug-prefix-map=${CMAKE_SOURCE_DIR}=.)

target_link_libraries(banana dobby)
target_link_libraries(banana ${CMAKE_CURRENT_SOURCE_DIR}/include/gd/libgame.so log android)

target_include_directories(banana PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/include/cocos2d/cocos2dx/include
    ${CMAKE_CURRENT_SOURCE_DIR}/include/cocos2d/cocos2dx
    ${CMAKE_CURRENT_SOURCE_DIR}/include/cocos2d/cocos2dx/platform/android
    ${CMAKE_CURRENT_SOURCE_DIR}/include/cocos2d/cocos2dx/kazmath/include
    ${CMAKE_CURRENT_SOURCE_DIR}/include/gd
    ${CMAKE_CURRENT_SOURCE_DIR}/include)