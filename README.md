# metadatos
language: cpp

git:
  quiet: true
  depth: 1

matrix:
  include:
    - os: linux
      dist: xenial
      sudo: required
      compiler: gcc
      env: COVERAGE=1 CMAKE_OPTIONS="-DCMAKE_BUILD_TYPE=Debug -DEXIV2_ENABLE_VIDEO=ON -DEXIV2_ENABLE_WEBREADY=ON -DEXIV2_BUILD_UNIT_TESTS=ON -DBUILD_WITH_COVERAGE=ON -DEXIV2_ENABLE_CURL=ON -DCMAKE_CXX_STANDARD=98"

    - os: linux
      dist: xenial
      sudo: required
      compiler: gcc
      env:
        - WITH_VALGRIND=1
        - CMAKE_OPTIONS="-DCMAKE_BUILD_TYPE=Release -DEXIV2_ENABLE_VIDEO=ON -DEXIV2_ENABLE_WEBREADY=ON -DEXIV2_BUILD_UNIT_TESTS=ON -DEXIV2_ENABLE_CURL=ON -DCMAKE_CXX_STANDARD=98"

    - os: linux
      dist: xenial
      sudo: required
      compiler: clang
      env: CMAKE_OPTIONS="-DCMAKE_BUILD_TYPE=Release -DEXIV2_ENABLE_VIDEO=ON -DEXIV2_ENABLE_WEBREADY=ON -DEXIV2_BUILD_UNIT_TESTS=ON -DEXIV2_ENABLE_CURL=ON -DCMAKE_CXX_STANDARD=98"

    - os: osx
      osx_image: xcode11.3
      compiler: clang
      env: CMAKE_OPTIONS="-DCMAKE_BUILD_TYPE=Release -DEXIV2_ENABLE_VIDEO=ON -DEXIV2_ENABLE_WEBREADY=ON -DEXIV2_BUILD_UNIT_TESTS=ON -DEXIV2_ENABLE_NLS=OFF -DEXIV2_ENABLE_CURL=ON -DCMAKE_CXX_STANDARD=98"

install: ./ci/install.sh
script:  ./ci/run.sh

cache:
    ccache: true
    directories:
    - conan         # Conan installation folder
    - $HOME/conanData     # Conan storage location
