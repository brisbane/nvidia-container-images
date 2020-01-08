FROM opensuse/leap
LABEL maintainer "NVIDIA CORPORATION <cudatools@nvidia.com>"

ENV GPUDK_URL http://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda-repo-opensuse15-10-2-local-10.2.89-440.33.01-1.0-1.x86_64.rpm
ENV CUDA_PKG_VERSION 10-2
ENV CUDA_CUBLAS_VERSION 10-0

COPY cuda.repo /etc/zypp/repos.d/cuda.repo

ENV CUDA_VERSION 10.2.89

ENV CUDA_PKG_VERSION 10-2-$CUDA_VERSION-1
# For libraries in the cuda-compat-* package: https://docs.nvidia.com/cuda/eula/index.html#attachment-a

RUN zypper --gpg-auto-import-keys ref -s

RUN zypper install -y \
      cuda-cudart-$CUDA_PKG_VERSION \
      cuda-compat-10-2 && \
    ln -s /usr/local/cuda-10.2 /usr/local/cuda && \
    zypper clean -a;

# nvidia-docker 1.0
RUN echo "/usr/local/nvidia/lib" >> /etc/ld.so.conf.d/nvidia.conf && \
    echo "/usr/local/nvidia/lib64" >> /etc/ld.so.conf.d/nvidia.conf

ENV PATH /usr/local/nvidia/bin:/usr/local/cuda/bin:${PATH}
ENV LD_LIBRARY_PATH /usr/local/nvidia/lib:/usr/local/nvidia/lib64

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES compute,utility
ENV NVIDIA_REQUIRE_CUDA "cuda>=10.2 brand=tesla,driver>=384,driver<385 brand=tesla,driver>=396,driver<397 brand=tesla,driver>=410,driver<411 brand=tesla,driver>=418,driver<419"


#RUN    zypper -n install \
#        cuda-nvrtc-$CUDA_PKG_VERSION \
#        cuda-cusolver-$CUDA_PKG_VERSION \
#        cuda-cublas-$CUDA_CUBLAS_VERSION \
#        cuda-cufft-$CUDA_PKG_VERSION \
#        cuda-curand-$CUDA_PKG_VERSION \
#        cuda-cusparse-$CUDA_PKG_VERSION \
#        cuda-npp-$CUDA_PKG_VERSION \
#        cuda-cudart-$CUDA_PKG_VERSION && \
#        cuda-compat-$CUDA_PKG_VERSION && \
#    ln -s /usr/local/cuda-10.2 /usr/local/cuda  &&\
#    zypper clean -a
     
