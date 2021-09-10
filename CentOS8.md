# Remote Provisioning Client (RPC)

RPC is an application which enables remote capabilities for AMT, such as as device activation. To accomplish this, RPC communicates with the RPS (Remote Provisioning Server).

The steps below assume the following directory structure where **rpc** is the clone of this repository, **vcpkg** is a clone of the VCPKG tool source and **build** is the RPC build directory. Both vcpkg and build directories will be created in later steps.

```
\rpc
  |__vcpkg
  |__build
```

# Linux

Steps below are for CentOS8.

## Dependencies

### CMake
Install CMake.
    
```
sudo yum install cmake
```

## Build C++ REST SDK

Using a Terminal window with the PATH and devtoolset enabled per the Dependencies.

```
git clone https://github.com/microsoft/vcpkg.git
cd vcpkg
git checkout 772d435ba18bf2f342458e0187ab7b48b84fe3f0
./bootstrap-vcpkg.sh
./vcpkg install cpprestsdk[websockets]
```

## Build RPC

Using a Terminal window with the PATH and devtoolset enabled per the Dependencies.

```
mkdir build
cd build
cmake -DCMAKE_TOOLCHAIN_FILE=/rpc/vcpkg/scripts/buildsystems/vcpkg.cmake -DCMAKE_BUILD_TYPE=Release ..
cmake --build .
```

To build debug:
```
cmake -DCMAKE_TOOLCHAIN_FILE=/rpc/vcpkg/scripts/buildsystems/vcpkg.cmake -DCMAKE_BUILD_TYPE=Debug ..
cmake --build .
```

## Run RPC

Open a Terminal window.

```
cd build
sudo ./rpc --url wss://localhost:8080 --cmd "-t activate --profile profile1"
```

Use --help for more options.
