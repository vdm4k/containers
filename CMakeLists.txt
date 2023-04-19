cmake_minimum_required(VERSION 3.14.0)
project(containers VERSION 1.0.0 DESCRIPTION "containers library" LANGUAGES CXX)

# core h files
set(H_FILES
    include/containers/mpmc_bounded_queue.h
)

add_library(${PROJECT_NAME} ${CPP_FILES} ${H_FILES})
add_library(bro::${PROJECT_NAME} ALIAS ${PROJECT_NAME})

target_compile_features(${PROJECT_NAME} PUBLIC cxx_std_17)
target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -Wpedantic -Wno-vla -Wno-unused-local-typedefs)

#sanitizer
option(WITH_SANITIZER "Enable address sanitizer" OFF)

if(WITH_SANITIZER)
    target_compile_options(${PROJECT_NAME} INTERFACE -fsanitize=address -fPIC)
    target_link_options(${PROJECT_NAME} INTERFACE -fsanitize=address)
endif()

target_link_libraries(${PROJECT_NAME} )
set_target_properties(${PROJECT_NAME} PROPERTIES LINKER_LANGUAGE CXX)
