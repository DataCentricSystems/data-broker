 #
 # Copyright © 2018 IBM Corporation
 #
 # Licensed under the Apache License, Version 2.0 (the "License");
 # you may not use this file except in compliance with the License.
 # You may obtain a copy of the License at
 #
 #    http://www.apache.org/licenses/LICENSE-2.0
 #
 # Unless required by applicable law or agreed to in writing, software
 # distributed under the License is distributed on an "AS IS" BASIS,
 # WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 # See the License for the specific language governing permissions and
 # limitations under the License.
 #

include( ${PROJECT_SOURCE_DIR}/backend/redis/libevent.cmake )

# prepare this RPATH stuff in case we need rpath in the test executables
# SET(CMAKE_SKIP_BUILD_RPATH  FALSE)
# SET(CMAKE_BUILD_WITH_INSTALL_RPATH FALSE) 
# SET(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib")


# define and add test sources

# test backend first
set(DB_BACKEND_TEST_SOURCES
	backend_common_request_queue_test.c
	backend_common_completion_queue_test.c
	backend_common_request_set_test.c
)

foreach(_test ${DB_BACKEND_TEST_SOURCES})
  get_filename_component(TEST_NAME ${_test} NAME_WE)
  add_executable(${TEST_NAME} ${_test})
  target_include_directories(${TEST_NAME} PRIVATE ${PROJECT_SOURCE_DIR}/test)
  add_test(DBBE_${TEST_NAME} ${TEST_NAME} )
  install(TARGETS ${TEST_NAME} RUNTIME
          DESTINATION test )
endforeach()
