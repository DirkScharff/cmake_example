cmake_minimum_required(VERSION 2.8.11)

# This should do it, shouldn't it?
set(CMAKE_LINK_DEPENDS_NO_SHARED 1)

Project(Example)

# dependency of the shared library:
file (GLOB libdep "library_dep/*.cpp" "library_dep/*.h")
include_directories(library_dep)
add_library(lib_dep ${libdep})

# shared library:
file (GLOB libsrc "library_src/*.cpp" "library_src/*.h")
include_directories(library_src)
add_library(example_lib SHARED ${libsrc})
target_link_libraries(example_lib lib_dep)
set_target_properties(example_lib PROPERTIES LINK_FLAGS ${LINK_FLAGS} "/export:f")

# executable:
file (GLOB exesrc "executable_src/*.cpp")
add_executable(example ${exesrc})
target_link_libraries(example example_lib)