#
#     Copyright 2013 Pixar
#
#     Licensed under the Apache License, Version 2.0 (the "License");
#     you may not use this file except in compliance with the License
#     and the following modification to it: Section 6 Trademarks.
#     deleted and replaced with:
#
#     6. Trademarks. This License does not grant permission to use the
#     trade names, trademarks, service marks, or product names of the
#     Licensor and its affiliates, except as required for reproducing
#     the content of the NOTICE file.
#
#     You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
#     Unless required by applicable law or agreed to in writing,
#     software distributed under the License is distributed on an
#     "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
#     either express or implied.  See the License for the specific
#     language governing permissions and limitations under the
#     License.
#

include_directories(
    ${PROJECT_SOURCE_DIR}/opensubdiv
    ${GLEW_INCLUDE_DIR}
    ${GLFW_INCLUDE_DIR}
)

set(SOURCE_FILES
    main.cpp
)

set(PLATFORM_LIBRARIES
    ${OSD_LINK_TARGET}
    ${OPENGL_LIBRARY}
    ${GLEW_LIBRARY}
    ${GLFW_LIBRARIES}
)

if ( OPENCL_FOUND )
    list(APPEND PLATFORM_LIBRARIES
        ${OPENCL_LIBRARIES}
    )
    include_directories( ${OPENCL_INCLUDE_DIRS} )
endif()


add_executable(osd_regression
    ${SOURCE_FILES}
)

add_dependencies(osd_regression blarg )

target_link_libraries(osd_regression
    ${PLATFORM_LIBRARIES}
)

install(TARGETS osd_regression DESTINATION ${CMAKE_BINDIR_BASE})
