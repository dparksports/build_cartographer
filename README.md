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
