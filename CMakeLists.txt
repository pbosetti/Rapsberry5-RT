cmake_minimum_required(VERSION 3.10)
project(TimerProject VERSION 1.0 LANGUAGES CXX)

option(ENABLE_RT_SCHEDULER "Enable real-time scheduler" ON)

if((APPLE OR WIN32) AND ENABLE_RT_SCHEDULER)
  message(FATAL_ERROR "Real-time scheduler is not supported on Apple or Windows platforms. Set ENABLE_RT_SCHEDULER to OFF.")
endif()

# Set C++17 standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Add executable
add_executable(timer timer.cpp)
if(ENABLE_RT_SCHEDULER)
  message(STATUS "Real-time scheduler enabled")
  target_compile_definitions(timer PRIVATE ENABLE_RT_SCHEDULER)
  target_link_libraries(timer PRIVATE rt)
endif()