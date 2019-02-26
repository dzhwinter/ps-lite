project(pslite CXX C)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake/Modules")
set(PS_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
set(PS_BINARY_DIR ${CMAKE_CURRENT_BINARY_DIR})
set(THIRD_PARTY ${CMAKE_SOURCE_DIR}/deps)

include_directories(${PS_SOURCE_DIR}/include)
include_directories(${PS_SOURCE_DIR}/src)

# third-party
include_directories(${THIRD_PARTY}/include)
link_directories(${THIRD_PARTY}/lib)

include(generic)
include(ProtoBuf)
include(${CMAKE_MODULE_PATH}/External/zmq)

option(WITH_TESTING     "Compile pslite with unit testing"        OFF)

set(COMMON_FLAGS
  -std=c++11
  -fPIC
  -fno-omit-frame-pointer
  )
foreach(flag ${COMMON_FLAGS})
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${flag}")
endforeach()


set(pslite_deps)

find_package(Protobuf REQUIRED)
include_directories(${Protobuf_INCLUDE_DIRS})
set(pslite_deps ${pslite_deps} ${Protobuf_LIBRARIES})

find_package(glog REQUIRED)
set(pslite_deps ${pslite_deps} glog::glog)

find_package(gflags REQUIRED)
set(pslite_deps ${pslite_deps} gflags::gflags)


find_library(ZMQ NAMES libzmq.a
  PATHS ${THIRD_PATRY}/lib NO_DEFAULT_PATH DOC "ZEROMQ library")

if(WITH_TESTING)
  enable_testing()
  find_package(gtest REQUIRED)
  set(pslite_deps ${pslite_deps} GTest::GTest GTest::Main)
endif()
