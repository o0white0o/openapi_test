cmake_minimum_required(VERSION 3.13)

set(MODULE_NAME openapi_test)
project(${MODULE_NAME})

set(NODE_VER 12)

set(NPX "npx")

find_program(NODEJS node)
find_program(NPXUTIL ${NPX})

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

if(NODEJS AND NPXUTIL)
    message(STATUS "NodeJS is Installed")
    execute_process(COMMAND npx -q check-node-version --node ">=${NODE_VER}" OUTPUT_VARIABLE NODE_VER_INSTALLED)
    #if(NOT NODE_VER_INSTALLED)
        message(STATUS "NodeJS has proper version")
        add_subdirectory(src)
    #else()
        message(WARNING "NodeJS has no proper version")
    #endif()
else()
    message(WARNING "NodeJS or npx utility is not installed")
endif()