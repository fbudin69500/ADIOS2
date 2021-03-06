#------------------------------------------------------------------------------#
# Distributed under the OSI-approved Apache License, Version 2.0.  See
# accompanying file Copyright.txt for details.
#------------------------------------------------------------------------------#

add_executable(TestUtilsCWriter TestUtilsCWriter.c)
target_link_libraries(TestUtilsCWriter adios2)

if(ADIOS2_HAVE_MPI)
  target_link_libraries(TestUtilsCWriter MPI::MPI_C)
  set(cmd_executor ${MPIEXEC_EXECUTABLE} ${MPIEXEC_NUMPROC_FLAG} 1)
else()
  set(cmd_executor)
endif()

add_test(NAME Utils.C.Writer
  COMMAND ${cmd_executor} $<TARGET_FILE:TestUtilsCWriter>
)
# This test produces TestUtilsCWriter.bp

# bpls -h
add_test(NAME Utils.Bpls.h.Dump
  COMMAND ${CMAKE_COMMAND}
    -DARGS=-h
    -DINPUT_FILE=TestUtilsCWriter.bp
    -DOUTPUT_FILE=TestUtilsCWriter.bplsh.result.txt
    -P "${PROJECT_BINARY_DIR}/$<CONFIG>/bpls.cmake"
)
set_property(TEST Utils.Bpls.h.Dump
  PROPERTY DEPENDS Utils.C.Writer
)

if(ADIOS2_HAVE_MPI)

add_test(NAME Utils.Bpls.h.Validate
  COMMAND ${CMAKE_COMMAND}
    -E compare_files
    ${CMAKE_CURRENT_SOURCE_DIR}/TestUtilsCWriter.bplsh.expected.txt
    ${CMAKE_CURRENT_BINARY_DIR}/TestUtilsCWriter.bplsh.result.txt
)
set_property(TEST Utils.Bpls.h.Validate
  PROPERTY DEPENDS Utils.Bpls.h.Dump
)

endif(ADIOS2_HAVE_MPI)


# bpls -la to screen for testing
add_test(NAME Utils.Bpls.la.Screen
  COMMAND ${CMAKE_COMMAND}
    -DARGS=-la
    -DINPUT_FILE=TestUtilsCWriter.bp
    -P "${PROJECT_BINARY_DIR}/$<CONFIG>/bpls.cmake"
)
set_property(TEST Utils.Bpls.la.Screen
  PROPERTY DEPENDS Utils.C.Writer
)


# bpls -la
add_test(NAME Utils.Bpls.la.Dump
  COMMAND ${CMAKE_COMMAND}
    -DARGS=-la
    -DINPUT_FILE=TestUtilsCWriter.bp
    -DOUTPUT_FILE=TestUtilsCWriter.bplsla.result.txt
    -P "${PROJECT_BINARY_DIR}/$<CONFIG>/bpls.cmake"
)
set_property(TEST Utils.Bpls.la.Dump
  PROPERTY DEPENDS Utils.C.Writer
)

if(ADIOS2_HAVE_MPI)

add_test(NAME Utils.Bpls.la.Validate
  COMMAND ${CMAKE_COMMAND}
    -E compare_files
    ${CMAKE_CURRENT_SOURCE_DIR}/TestUtilsCWriter.bplsla.expected.txt
    ${CMAKE_CURRENT_BINARY_DIR}/TestUtilsCWriter.bplsla.result.txt
)
set_property(TEST Utils.Bpls.la.Validate
  PROPERTY DEPENDS Utils.Bpls.la.Dump
)

endif(ADIOS2_HAVE_MPI)


# bpls -Al
add_test(NAME Utils.Bpls.Al.Dump
  COMMAND ${CMAKE_COMMAND}
    -DARGS=-Al
    -DINPUT_FILE=TestUtilsCWriter.bp
    -DOUTPUT_FILE=TestUtilsCWriter.bplsAl.result.txt
    -P "${PROJECT_BINARY_DIR}/$<CONFIG>/bpls.cmake"
)
set_property(TEST Utils.Bpls.Al.Dump
  PROPERTY DEPENDS Utils.C.Writer
)

if(ADIOS2_HAVE_MPI)

add_test(NAME Utils.Bpls.Al.Validate
  COMMAND ${CMAKE_COMMAND}
    -E compare_files
    ${CMAKE_CURRENT_SOURCE_DIR}/TestUtilsCWriter.bplsAl.expected.txt
    ${CMAKE_CURRENT_BINARY_DIR}/TestUtilsCWriter.bplsAl.result.txt
)
set_property(TEST Utils.Bpls.Al.Validate
  PROPERTY DEPENDS Utils.Bpls.Al.Dump
)

endif(ADIOS2_HAVE_MPI)

# bpls -ldDav
add_test(NAME Utils.Bpls.ldDav.Dump
  COMMAND ${CMAKE_COMMAND}
    -DARGS='-ldDav'
    -DINPUT_FILE=TestUtilsCWriter.bp
    -DOUTPUT_FILE=TestUtilsCWriter.bplsldDav.result.txt
    -P "${PROJECT_BINARY_DIR}/$<CONFIG>/bpls.cmake"
)
set_property(TEST Utils.Bpls.ldDav.Dump
  PROPERTY DEPENDS Utils.C.Writer
)

if(ADIOS2_HAVE_MPI)

add_test(NAME Utils.Bpls.ldDav.Validate
  COMMAND ${CMAKE_COMMAND}
    -E compare_files
    ${CMAKE_CURRENT_SOURCE_DIR}/TestUtilsCWriter.bplsldDav.expected.txt
    ${CMAKE_CURRENT_BINARY_DIR}/TestUtilsCWriter.bplsldDav.result.txt
)
set_property(TEST Utils.Bpls.ldDav.Validate
  PROPERTY DEPENDS Utils.Bpls.ldDav.Dump
)


endif(ADIOS2_HAVE_MPI)


# bpls -ldDavvv
add_test(NAME Utils.Bpls.ldDavvv.Dump
  COMMAND ${CMAKE_COMMAND}
    -DARGS='-ldDavvv'
    -DINPUT_FILE=TestUtilsCWriter.bp
    -DOUTPUT_FILE=TestUtilsCWriter.bplsldDavvv.result.txt
    -P "${PROJECT_BINARY_DIR}/$<CONFIG>/bpls.cmake"
)
set_property(TEST Utils.Bpls.ldDavvv.Dump
  PROPERTY DEPENDS Utils.C.Writer
)

if(ADIOS2_HAVE_MPI)

add_test(NAME Utils.Bpls.ldDavvv.Validate
  COMMAND ${CMAKE_COMMAND}
    -E compare_files
    ${CMAKE_CURRENT_SOURCE_DIR}/TestUtilsCWriter.bplsldDavvv.expected.txt
    ${CMAKE_CURRENT_BINARY_DIR}/TestUtilsCWriter.bplsldDavvv.result.txt
)
set_property(TEST Utils.Bpls.ldDavvv.Validate
  PROPERTY DEPENDS Utils.Bpls.ldDavvv.Dump
)


endif(ADIOS2_HAVE_MPI)


# bpls -ld varI16 -n 10
#add_test(NAME Utils.Bpls.ldvarI16.Dump
#  COMMAND ${CMAKE_COMMAND}
#    -DARGS=-ld varI16 -n 10
#    -DINPUT_FILE=TestUtilsCWriter.bp
#    -DOUTPUT_FILE=TestUtilsCWriter.bplsldvarI16.result.txt
#    -P "${PROJECT_BINARY_DIR}/$<CONFIG>/bpls.cmake"
#)
#set_property(TEST Utils.Bpls.la.Dump
#  PROPERTY DEPENDS Utils.C.Writer
#)
#
#add_test(NAME Utils.Bpls.ldvarI16.Validate
#  COMMAND ${CMAKE_COMMAND}
#    -E compare_files
#    ${CMAKE_CURRENT_SOURCE_DIR}/TestUtilsCWriter.bplsldvarI16.expected.txt
#    ${CMAKE_CURRENT_BINARY_DIR}/TestUtilsCWriter.bplsldvarI16.result.txt
#)
#set_property(TEST Utils.Bpls.ldvarI16.Validate
#  PROPERTY DEPENDS Utils.Bpls.ldvarI16.Dump
#)




if(ADIOS2_HAVE_MPI)
  add_subdirectory(iotest)
endif(ADIOS2_HAVE_MPI)
