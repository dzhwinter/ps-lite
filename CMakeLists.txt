cmake_minimum_required(VERSION 3.10)
project(ps_lite)

set(CMAKE_CXX_STANDARD 14)

include_directories(deps)
include_directories(deps/include)
include_directories(include)
include_directories(include/dmlc)
include_directories(include/ps)
include_directories(include/ps/internal)
include_directories(src)
include_directories(src/windows)

add_executable(ps_lite
        deps/include/zmq.h
        deps/include/zmq_utils.h
        include/dmlc/base.h
        include/dmlc/logging.h
        include/ps/internal/assign_op.h
        include/ps/internal/customer.h
        include/ps/internal/env.h
        include/ps/internal/message.h
        include/ps/internal/parallel_kv_match.h
        include/ps/internal/parallel_sort.h
        include/ps/internal/postoffice.h
        include/ps/internal/threadsafe_queue.h
        include/ps/internal/utils.h
        include/ps/internal/van.h
        include/ps/base.h
        include/ps/kv_app.h
        include/ps/ps.h
        include/ps/range.h
        include/ps/sarray.h
        include/ps/simple_app.h
        src/windows/unistd.h
        src/customer.cc
        src/network_utils.h
        src/postoffice.cc
        src/resender.h
        src/van.cc
        src/zmq_van.h
        tests/test_connection.cc
        tests/test_kv_app.cc
        tests/test_kv_app_multi_workers.cc
        tests/test_simple_app.cc)
