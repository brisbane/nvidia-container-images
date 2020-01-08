FROM cuda:10.2-runtime-opensuse-leap15.1
LABEL maintainer "NVIDIA CORPORATION <sw-cuda-installer@nvidia.com>"

RUN zypper install -y \
        cuda-nvml-dev-$CUDA_PKG_VERSION \
        cuda-command-line-tools-$CUDA_PKG_VERSION \
cuda-libraries-dev-$CUDA_PKG_VERSION \
        cuda-minimal-build-$CUDA_PKG_VERSION \
        libcublas-devel-10.2.2.89-1 \
        &&  ln -sf sr/local/cuda-10.2 /usr/local/cuda 

ENV LIBRARY_PATH /usr/local/cuda/lib64/stubs
