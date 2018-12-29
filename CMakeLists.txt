option(
  SHA3_USE_KECCAK
  "Use the Keccak variant, 0x6 rather than 0x1 for padding prefix"
  ON
)

add_library(SHA3IUF STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sha3.c)
target_include_directories(SHA3IUF PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

if(${SHA3_USE_KECCAK})
	target_compile_definitions(SHA3IUF PRIVATE SHA3_USE_KECCAK=1)
endif()

add_executable(sha3sum ${CMAKE_CURRENT_SOURCE_DIR}/sha3sum.c)
target_link_libraries(sha3sum SHA3IUF)

add_executable(sha3test ${CMAKE_CURRENT_SOURCE_DIR}/sha3test.c)
target_link_libraries(sha3test SHA3IUF)
add_test(NAME run_sha3test COMMAND sha3test)
