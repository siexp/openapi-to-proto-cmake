# Usage
example CMakeLists.txt 
```
cmake_minimum_required(VERSION 3.21.0)
project(api.protobuf)

set(CMAKE_CXX_STANDARD 20)

find_package(Protobuf REQUIRED)

ExternalProject_Add(OpenapiToProto
  GIT_REPOSITORY git@github.com:siexp/openapi-to-proto-cmake.git
)
include(OpenapiToProto/OpenapiToProto.cmake)
file(GLOB YAMLS "*.yaml" "*.yml")
openapi_to_proto(PROTOS ${YAMLS})

protobuf_generate_cpp(PROTO_SRCS PROTO_HDRS ${PROTOS})

add_library(api.protobuf STATIC ${PROTO_SRCS} ${PROTO_HDRS})
```