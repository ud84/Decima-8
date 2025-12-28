cmake_minimum_required(VERSION 3.20)
project(H323_26 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(FetchContent)
FetchContent_Declare(
  Catch2
  GIT_REPOSITORY https://github.com/catchorg/Catch2.git
  GIT_TAG        v3.4.0
)
FetchContent_MakeAvailable(Catch2)

add_subdirectory(src)
enable_testing()
add_subdirectory(tests)


cmake_minimum_required(VERSION 3.28) # Для стабильной поддержки модулей
project(Decima8 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Включаем поддержку модулей для Clang/MSVC/GCC
add_library(nbe_core)
target_sources(nbe_core
    PUBLIC FILE_SET CXX_MODULES FILES
    src/Core.ixx
    src/Hardware.ixx
    src/Circuit.ixx
)

add_executable(decima_bin src/Main.cpp)
target_link_libraries(decima_bin PRIVATE nbe_core)
