
cmake_minimum_required(VERSION 3.22.1)

project("proofofpassport")

include_directories(include)

link_directories(lib)

add_library(rapidsnark SHARED IMPORTED)
set_target_properties(rapidsnark PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/lib/librapidsnark.so)


add_library(register_sha256WithRSAEncryption_65537 SHARED IMPORTED)
set_target_properties(register_sha256WithRSAEncryption_65537 PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/lib/libwitnesscalc_register_sha256WithRSAEncryption_65537.so)

add_library(disclose SHARED IMPORTED)
set_target_properties(disclose PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/lib/libwitnesscalc_disclose.so)

add_library(${CMAKE_PROJECT_NAME} SHARED
        proofofpassport.cpp)

target_link_libraries(${CMAKE_PROJECT_NAME}
        rapidsnark register_sha256WithRSAEncryption_65537 disclose)
