CMAKE_MINIMUM_REQUIRED( VERSION 3.7 )
PROJECT( linenoise )

SET( CMAKE_C_STANDARD 11 )
SET( CMAKE_CXX_STANDARD 17 )

ADD_DEFINITIONS( -W -Wall -Wextra )

# build liblinenoise
ADD_LIBRARY( linenoise STATIC
  src/ConvertUTF.cpp
  src/linenoise.cpp
  src/wcwidth.cpp
)
IF( CMAKE_COMPILER_IS_GNUCC )
  TARGET_COMPILE_OPTIONS( linenoise PRIVATE 
    -Wno-implicit-fallthrough
  )
ENDIF()
TARGET_INCLUDE_DIRECTORIES( linenoise PUBLIC
  ${CMAKE_CURRENT_SOURCE_DIR}/include 
)

# build example
IF( BUILD_TESTS )
  ADD_EXECUTABLE( linenoise-example tst/example.c )
  TARGET_LINK_LIBRARIES( linenoise-example linenoise
)
ENDIF()
