add_library(utils
eigendecomposition.cpp eigendecomposition.h
gzstream.cpp gzstream.h
optimization.cpp optimization.h
stoprule.cpp stoprule.h
tools.cpp tools.h
pllnni.cpp pllnni.h
checkpoint.cpp checkpoint.h
MPIHelper.cpp MPIHelper.h
starttree.cpp starttree.h
bionj.cpp bionj2.cpp bionj2.h
progress.cpp progress.h
timeutil.h hammingdistance.h
operatingsystem.cpp operatingsystem.h
heapsort.h
)

if(ZLIB_FOUND)
  target_link_libraries(utils ${ZLIB_LIBRARIES})
else(ZLIB_FOUND)
  target_link_libraries(utils zlibstatic)
endif(ZLIB_FOUND)

target_link_libraries(utils lbfgsb sprng)

##################################################################
# Whether to build the decenttree executable file (default: ON)
##################################################################
option(BUILD_DECENTTREE "build decenttree" ON)

if(BUILD_DECENTTREE)
  add_executable(decentTree
    decenttree.cpp
    starttree.cpp bionj.cpp bionj2.cpp
    gzstream.cpp progress.cpp operatingsystem.cpp)
endif(BUILD_DECENTTREE)

if(ZLIB_FOUND)
  target_link_libraries(decentTree ${ZLIB_LIBRARIES})
else(ZLIB_FOUND)
  target_link_libraries(decentTree zlibstatic)
endif(ZLIB_FOUND)

if(CLANG AND WIN32)
  target_link_libraries(decentTree ${PROJECT_SOURCE_DIR}/lib/libiomp5md.dll)
endif()
