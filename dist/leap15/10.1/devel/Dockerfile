ARG IMAGE_NAME
FROM ${IMAGE_NAME}:10.1-runtime-leap15
LABEL maintainer "NVIDIA CORPORATION <sw-cuda-installer@nvidia.com>"

RUN zypper install -y \
        cuda-nvml-dev-$CUDA_PKG_VERSION \
        cuda-command-line-tools-$CUDA_PKG_VERSION \
cuda-libraries-dev-$CUDA_PKG_VERSION \
        cuda-minimal-build-$CUDA_PKG_VERSION \
        libcublas-devel-10.2.1.243-1 \
        ;\
        zypper clean -a && \
        ldconfig

ENV LIBRARY_PATH /usr/local/cuda/lib64/stubs