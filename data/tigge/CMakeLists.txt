# data/tigge/CMakeLists.txt
# Download all the TIGGE grib data from website

file(READ "tigge_data_files.txt" tigge_files_to_download)
string(REGEX REPLACE "\n" ";" tigge_files_to_download "${tigge_files_to_download}")

if( ENABLE_EXTRA_TESTS )
    # Download all data files
    ecbuild_get_test_multidata( TARGET eccodes_download_tigge_gribs
                            NOCHECK
                            NAMES ${tigge_files_to_download} )
endif()

#######
# Copy other files - e.g. reference data, text files etc from the source data dir
list(APPEND other_files
    tigge_data_files.txt)
foreach( file ${other_files} )
   execute_process( COMMAND ${CMAKE_COMMAND} -E copy_if_different ${CMAKE_CURRENT_SOURCE_DIR}/${file} ${CMAKE_CURRENT_BINARY_DIR} )
endforeach()
