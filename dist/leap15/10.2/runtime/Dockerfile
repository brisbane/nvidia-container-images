FROM cuda:10.2-base-opensuse-leap15.1
LABEL maintainer "NVIDIA CORPORATION <sw-cuda-installer@nvidia.com>"

RUN zypper install -y \
        cuda-libraries-$CUDA_PKG_VERSION \
cuda-nvtx-$CUDA_PKG_VERSION \
    libcublas10-10.2.2.89-1 

RUN zypper clean -a; \
    ldconfg

