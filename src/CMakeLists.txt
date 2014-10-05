set(alignment_source_files
kseq.h
ssw.c
ssw.h
ssw_cpp.cpp
ssw_cpp.h
	)
set(main_src
main.cpp)

add_library(libssw ${alignment_source_files})
add_executable(ssw_run ${main_src})


target_link_libraries(ssw_run libssw)

include_directories( ${ZLIB_INCLUDE_DIRS} )
target_link_libraries( ssw_run ${ZLIB_LIBRARIES} )
target_link_libraries( ssw_run ${M_LIB})