cmake_minimum_required(VERSION 3.12)
project(opencryptoki)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

set(GTEST_DIR gtest-1.10.0/googletest)
set(GTEST_INC -isystem ${GTEST_DIR}/include)

add_executable(pkcs11test
        pkcs11test.cc
        pkcs11-describe.cc
        describe.cc
        globals.cc
        init.cc
        slot.cc
        session.cc
        object.cc
        login.cc
        rng.cc
        tookan.cc
        keypair.cc
        cipher.cc
        digest.cc
        sign.cc
        hmac.cc
        key.cc
        dual.cc
)
target_include_directories(pkcs11test PRIVATE third_party/pkcs11)
target_link_libraries(pkcs11test PRIVATE gtest dl pthread)

add_library(gtest STATIC ${GTEST_DIR}/src/gtest-all.cc)
target_include_directories(gtest PUBLIC ${GTEST_INC} PRIVATE ${GTEST_DIR})
