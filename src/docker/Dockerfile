FROM emscripten/emsdk:3.1.45

RUN git clone -b 4.8.0 https://github.com/opencv/opencv --depth 1

RUN apt-get -qq -y update && apt-get -qq install -y --no-install-recommends \
        wget \
        git-core \
        ca-certificates \
        build-essential \
        file 

ARG BUILD_TYPE=Release

RUN cd opencv && \
    mkdir build && \
    cd build && \
    cmake .. \
        -DCMAKE_INSTALL_PREFIX=/usr/local \
        -DCMAKE_BUILD_TYPE=$BUILD_TYPE \
        -DCMAKE_TOOLCHAIN_FILE='/emsdk/upstream/emscripten/cmake/Modules/Platform/Emscripten.cmake' \
        -DCMAKE_CXX_FLAGS='-O3' \
        -DCMAKE_C_FLAGS='-O3' \
        -DSTATIC_LIBRARY_FLAGS='-lembind -s ASSERTIONS=1 --memory-init-file 0 -s ERROR_ON_UNDEFINED_SYMBOLS=0' \
        -DCPU_BASELINE='' \
        -DCPU_DISPATCH='' \
        -DCV_TRACE=OFF \
        -DBUILD_SHARED_LIBS=OFF \
        -DWITH_1394=OFF \
        -DWITH_ADE=OFF \
        -DWITH_VTK=OFF \
        -DWITH_EIGEN=OFF \
        -DWITH_FFMPEG=OFF \
        -DWITH_GSTREAMER=OFF \
        -DWITH_GTK=OFF \
        -DWITH_GTK_2_X=OFF \
        -DWITH_IPP=OFF \
        -DWITH_JASPER=OFF \
        -DWITH_JPEG=OFF \
        -DWITH_WEBP=OFF \
        -DWITH_OPENEXR=OFF \
        -DWITH_OPENGL=OFF \
        -DWITH_OPENVX=OFF \
        -DWITH_OPENNI=OFF \
        -DWITH_OPENNI2=OFF \
        -DWITH_PNG=OFF \
        -DWITH_TBB=OFF \
        -DWITH_TIFF=OFF \
        -DWITH_V4L=OFF \
        -DWITH_OPENCL=OFF \
        -DWITH_OPENCL_SVM=OFF \
        -DWITH_OPENCLAMDFFT=OFF \
        -DWITH_OPENCLAMDBLAS=OFF \
        -DWITH_GPHOTO2=OFF \
        -DWITH_LAPACK=OFF \
        -DWITH_ITT=OFF \
        -DWITH_QUIRC=OFF \
        -DWITH_PTHREADS_PF=OFF \
        -DBUILD_ZLIB=OFF \
        -DBUILD_opencv_apps=OFF \
        -DBUILD_opencv_calib3d=OFF \
        -DBUILD_opencv_core=ON \
        -DBUILD_opencv_dnn=OFF \
        -DBUILD_opencv_features2d=OFF \
        -DBUILD_opencv_flann=OFF \  
        -DBUILD_opencv_gapi=OFF \
        -DBUILD_opencv_ml=OFF \
        -DBUILD_opencv_photo=OFF \
        -DBUILD_opencv_imgcodecs=OFF \
        -DBUILD_opencv_imgproc=ON \
        -DBUILD_opencv_shape=OFF \
        -DBUILD_opencv_video=OFF \
        -DBUILD_opencv_videoio=OFF \
        -DBUILD_opencv_videostab=OFF \
        -DBUILD_opencv_highgui=OFF \
        -DBUILD_opencv_superres=OFF \
        -DBUILD_opencv_stitching=OFF \
        -DBUILD_opencv_ts=OFF \
        -DBUILD_opencv_java=OFF \
        -DBUILD_opencv_java_bindings_generator=OFF \
        -DBUILD_opencv_js=OFF \
        -DBUILD_opencv_python2=OFF \
        -DBUILD_opencv_python3=OFF \
        -DBUILD_opencv_python_bindings_generator=OFF \
        -DBUILD_EXAMPLES=OFF \
        -DBUILD_PACKAGE=OFF \
        -DBUILD_TESTS=OFF \
        -DBUILD_PERF_TESTS=OFF \
        -DBUILD_FAT_JAVA_LIB=OFF \
        -DBUILD_CUDA_STUBS=OFF \
        -DBUILD_DOCS=OFF \
        -DBUILD_IPP_IW=OFF \
        -DBUILD_ITT=OFF \
        -DBUILD_JASPER=OFF \
        -DBUILD_JAVA=OFF \
        -DBUILD_JPEG=OFF \
        -DBUILD_OPENEXR=OFF \
        -DBUILD_PNG=OFF \
        -DBUILD_PROTOBUF=OFF \
        -DBUILD_TBB=OFF \
        -DBUILD_TIFF=OFF \
        -DBUILD_WITH_DEBUG_INFO=OFF \
        -DBUILD_WITH_DYNAMIC_IPP=OFF \
        -DWITH_OPENMP=OFF \
        -DCV_ENABLE_INTRINSICS=OFF &&\
        make -j8 &&\
        make install &&\
        rm -rf /src

ENV CC=emcc
ENV AR=emar
RUN git clone --depth 1 --branch v1.5.5 https://github.com/facebook/zstd.git /zstd && cd /zstd && make 
