cmake_minimum_required(VERSION 3.2)

PROJECT(nnet3-xvector-class)
set(CMAKE_C_COMPILER gcc)
set(CMAKE_CXX_COMPILER g++)
set(CMAKE_CXX_STANDARD 11)
add_definitions(-msse
        -msse2
        -pthread
        -g
        -fPIC
        -D HAVE_CUDA
        -Wno-sign-compare
        -Wall
        -Wno-sign-compare
        -Wno-unused-local-typedefs
        -Wno-deprecated-declarations
        -Winit-self
        -D KALDI_DOUBLEPRECISION=0
        -D HAVE_EXECINFO_H=1
        -D HAVE_CXXABI_H
        -D HAVE_ATLAS)
# g++  -Wl,-rpat  nnet3-xvector-compute.o   ../nnet3/libkaldi-nnet3.so  ../chain/libkaldi-chain.so  ../cudamatrix/libkaldi-cudamatrix.so  ../decoder/libkaldi-decoder.so  ../lat/libkaldi-lat.so  ../fstext/libkaldi-fstext.so  ../hmm/libkaldi-hmm.so  ../transform/libkaldi-transform.so  ../gmm/libkaldi-gmm.so  ../tree/libkaldi-tree.so  ../util/libkaldi-util.so  ../matrix/libkaldi-matrix.so  ../base/libkaldi-base.so /home/shi/guiji/kaldi-master/tools/openfst/lib/libfst.so /usr/lib/libatlas.so.3 /usr/lib/libf77blas.so.3 /usr/lib/libcblas.so.3 /usr/lib/liblapack_atlas.so.3 -lm -lpthread -ldl -lcublas -lcusparse -lcudart -lcurand  -o nnet3-xvector-compute
link_directories(
        /home/shi/guiji/kaldi-master/tools/openfst/lib
        /home/shi/guiji/kaldi-master/src/lib
        /usr/local/cuda/lib64

)
include_directories(
        /usr/include
        /home/shi/guiji/kaldi-master/src/
        /usr/local/cuda/include/
        /home/shi/guiji/kaldi-master/tools/ATLAS_headers/include
        /home/shi/guiji/kaldi-master/tools/openfst/include
)

set(nnet_src

        /home/shi/guiji/kaldi-master/src/nnet3bin/nnet3-xvector-class.cc

        )
add_library(nnet3-xvector-class SHARED ${nnet_src} )

target_link_libraries(nnet3-xvector-class
        kaldi-nnet3
        kaldi-feat
        kaldi-chain
        kaldi-cudamatrix
        kaldi-decoder
        kaldi-lat
        kaldi-fstext
        kaldi-hmm
        kaldi-transform
        kaldi-gmm
        kaldi-tree
        kaldi-util
        kaldi-matrix
        kaldi-base
        m  pthread    cublas cusparse cudart curand  openblas  -dl)


