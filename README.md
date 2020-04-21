# build_cartographer

You can do it just with cmake without ninja. Install these:

sudo apt-get install autoconf \
automake \
build-essential \
clang \
clang-format \
cmake \
cmake-curses-gui \
curl \
g++ \
git \
gitk  \
google-mock \
kcachegrind \
libboost-all-dev \
libc++-dev \
libcairo2-dev \
libeigen3-dev \
libgflags-dev \
libgtest-dev \
libgoogle-glog-dev \
liblua5.2-dev \
libsuitesparse-dev \
libtool \
make \
meld \
ninja-build \
python-rosdep \
python-sphinx
python-wstool \
stow \
unzip \
valgrind

Ok, now let's start from scratch.

Ceres part:

git clone https://github.com/ceres-solver/ceres-solver.git
cd ceres-solver
mkdir build && cd build
cmake .. -G Ninja -DCXX11=ON -DCMAKE_INSTALL_PREFIX=/usr/local/stow/ceres
cd /usr/local/stow/
sudo stow ceres

Cartographer part:

git@github.com:googlecartographer/cartographer.git
cd cartographer
mkdir build
cd build
cmake ..
make -j10


wget https://github.com/protocolbuffers/protobuf/releases/download/v3.6.1/protobuf-cpp-3.6.1.tar.gz

tar -xvf protobuf-cpp-3.6.1.tar.gz
cd protobuf-3.6.1 
./configure --disable-shared CXXFLAGS="-fPIC"
make -j8 

    tips: we compile static library with --disable-shared CXXFLAGS="-fPIC". 编译动态库dll/so的时候，如果依赖static library(比如profobuf)，那么static library编译的时候需要加上-fPIC,否则动态库编译出错。
    对于CMake,使用cmake CMAKE_CXX_FLGAS="-fPIC" ..

otherwise, error occurs

Linking CXX shared library ../../../../bin/libcommon.so
/usr/bin/ld: /usr/local/lib/libprotobuf.a(common.o): relocation R_X86_64_32S against `.rodata' can not be used when makinga shared object; recompile with -fPIC
/usr/local/lib/libprotobuf.a: error adding symbols: Bad value

install

sudo make install
sudo ldconfig

sudo make uninstall


