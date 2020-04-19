cmake_minimum_required(VERSION 3.5)

if (BOOST_DIR)
  set(BOOST_ROOT ${BOOST_DIR})
endif (BOOST_DIR)

# Find python and Boost - both are required dependencies
find_package(PythonLibs 2.7 REQUIRED)
find_package(Boost COMPONENTS python27 REQUIRED)

# Without this, any build libraries automatically have names "lib{x}.so"
set(CMAKE_SHARED_MODULE_PREFIX "")

# Add a shared module - modules are intended to be imported at runtime.
# - This is where you add the source files
add_library(hello_ext MODULE pythonWrapper.cpp)

# Set up the libraries and header search paths for this target
target_link_libraries(hello_ext ${Boost_LIBRARIES} ${PYTHON_LIBRARIES})
target_include_directories(hello_ext PRIVATE ${Boost_INCLUDE_DIRS} ${PYTHON_INCLUDE_DIRS})

