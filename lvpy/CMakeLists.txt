find_package(Python COMPONENTS Interpreter NumPy REQUIRED)
include_directories(${PYTHON_INCLUDE_PATH})

find_package(SWIG 4.0 COMPONENTS python REQUIRED)
include(${SWIG_USE_FILE})

set(USE_SWIG_DEPENDENCIES TRUE)

set(SRC lv.i)

set_source_files_properties(${SRC} PROPERTIES CPLUSPLUS ON)

swig_add_library(lvpy TYPE MODULE LANGUAGE python SOURCES ${SRC})

target_link_libraries(lvpy
        PUBLIC lv
               Python::Module
               Python::NumPy)

# See https://gitlab.kitware.com/cmake/cmake/-/issues/18003
set_target_properties(lvpy PROPERTIES SWIG_USE_TARGET_INCLUDE_DIRECTORIES TRUE)
