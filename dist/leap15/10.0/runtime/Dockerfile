ARG IMAGE_NAME
FROM ${IMAGE_NAME}:10.0-base-leap15
LABEL maintainer "NVIDIA CORPORATION <sw-cuda-installer@nvidia.com>"

RUN zypper -n install -y \
        cuda-libraries-$CUDA_PKG_VERSION \
        cuda-nvtx-$CUDA_PKG_VERSION \
    && \
    zypper clean -a && \
    ldconfig 