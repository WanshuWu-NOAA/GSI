cmake_minimum_required(VERSION 2.6)
if(BUILD_UTIL)
  file(GLOB LOCAL_SRC ${CMAKE_CURRENT_SOURCE_DIR}/*.f90)
  list( REMOVE_ITEM LOCAL_SRC ${CMAKE_CURRENT_SOURCE_DIR}/main.f90 )
  set_source_files_properties( ${LOCAL_SRC} PROPERTIES COMPILE_FLAGS ${GSI_Fortran_FLAGS} )
  add_executable(calc_increment_ncio.x  ${LOCAL_SRC} )
  set_target_properties( calc_increment_ncio.x PROPERTIES COMPILE_FLAGS ${UTIL_Fortran_FLAGS} )
  SET( CMAKE_EXE_LINKER_FLAGS  "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_Fortran_FLAGS}" )
  include_directories( ${UTIL_INC} ${NEMSIOINC} ${NETCDF_INCLUDE_DIRS} ${MPI_Fortran_INCLUDE_PATH} ${FV3GFS_NCIO_INCS}) 
  target_link_libraries( calc_increment_ncio.x ${CORE_LIBRARIES} ${NETCDF_Fortran_LIBRARIES} ${NETCDF_C_LIBRARIES} ${MPI_Fortran_LIBRARIES} ${FV3GFS_NCIO_LIBRARIES} )
endif()
