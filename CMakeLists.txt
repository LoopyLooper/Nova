## NOVA_ROOT_CMAKE

cmake_minimum_required(VERSION 3.20)

set(PNAME "Nova")
project(${PNAME})


## Other settings
set(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)

set(CMAKE_TOOLCHAIN_FILE "C:/Users/Loop/Desktop/Others/Utilities/Tools/Vcpkg/scripts/buildsystems/vcpkg.cmake")
set(VCPKG_TARGET_TRIPLET "x64-windows")

set(CMAKE_CXX_STANDARD 20)


## Source files
set(SRC_FILES
	"tests.cpp"
)
list(TRANSFORM SRC_FILES PREPEND "src/")

add_executable(${PNAME} ${SRC_FILES})


## Include directories
target_include_directories(${PNAME} PRIVATE "include/" "src/")


## Libraries
find_package(fmt CONFIG REQUIRED)
find_package(glm CONFIG REQUIRED)
find_package(glad CONFIG REQUIRED)
find_package(glfw3 CONFIG REQUIRED)
target_link_libraries(${PNAME} PRIVATE fmt::fmt glm::glm glad::glad glfw)


## Compile options
if(MSVC)
	target_compile_options(${PNAME} PRIVATE /W4 /w14640 /WX)
else()
	target_compile_options(${PNAME} PRIVATE -Wall -Wextra -Wshadow -Wnon-virtual-dtor -pedantic -Werror)
endif()
