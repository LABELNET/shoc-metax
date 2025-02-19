
The Scalable HeterOgeneous Computing (SHOC) benchmark suite is a
collection of benchmark programs testing the performance and
stability of systems using computing devices with non-traditional architectures
for general purpose computing. Its initial focus is on systems containing
Graphics Processing Units (GPUs) and multi-core processors, and on the
OpenCL programming standard. It can be used on clusters as well as individual
hosts.

Documentation on configuring, building, and running the SHOC benchmark
programs is contained in the SHOC user manual, in the doc subdirectory
of the SHOC source code tree.  The file INSTALL.txt contains a sketch of
those instructions for rapid installation.

Installation should be familiar to anyone who is experienced with configure
and make, see the config directory for some examples.  Also, if your
platform requires regenerating the configure script, see build-aux/bootstrap.sh
and the manual for more details.

Last update: 2014-04-13 15:39:22 kspaff


Metax C500 测试过程

## 环境

```
source mx-envs.sh
source cmake_maca
source make_maca
```

当前目录应看见 `CUDA_DIR` 目录

## 编译

shoc 目录，进行配置和编译

```
./configure  --with-cuda \
--without-opencl \
--without-mpi \
--disable-stability \
CPPFLAGS="-I/opt/maca/include -I/opt/maca/include/mcr -I$HOME/cu-bridge/CUDA_DIR/include" \
CUDA_CPPFLAGS="" \
LIBS="-lcuda -lcudart" \
LDFLAGS="-L$HOME/cu-bridge/CUDA_DIR/lib64" \
NVCC="$HOME/cu-bridge/CUDA_DIR/bin/nvcc" 

# 编译
make_maca 
make_maca install
```

## 运行

进入 bin 目录

- cuda 全部用例

```
./shocdriver -s 1 -d 0 -cuda
```

- cuda 单个用例

```
./shocdriver -s 1 -d 0 -cuda -benchmark MaxFlops
```

