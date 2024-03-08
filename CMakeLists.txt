cmake_minimum_required(VERSION 3.10)
project(base-workflow)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(SOGOU_WF_PATH "/root/github-project/workflow")

find_package(OpenSSL REQUIRED)

add_library(workflow STATIC IMPORTED)
set_target_properties(workflow PROPERTIES IMPORTED_LOCATION ${SOGOU_WF_PATH}/_lib/libworkflow.a)
target_include_directories(workflow INTERFACE ${SOGOU_WF_PATH}/_include)

add_executable(base-workflow main.cc)
target_link_libraries(base-workflow PRIVATE pthread OpenSSL::SSL OpenSSL::Crypto rt)
target_link_libraries(base-workflow PRIVATE workflow)