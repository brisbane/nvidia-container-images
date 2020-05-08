FROM opensuse/leap:15
LABEL maintainer "NVIDIA CORPORATION <cudatools@nvidia.com>"

RUN zypper -n install -y curl && mkdir -p /etc/pki/rpm-gpg
ENV GPUDK_URL http://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda-repo-opensuse15-10-2-local-10.2.89-440.33.01-1.0-1.x86_64.rpm
ENV CUDA_VERSION 10.0.130
ENV CUDA_PKG_VERSION 10-0

RUN echo $'[cuda]\n\
name=cuda\n\
enabled=1\n\
autorefresh=0\n\
baseurl=https://developer.download.nvidia.com/compute/cuda/repos/opensuse15/x86_64/\n\
type=rpm-md\n\
gpgcheck=1\n\
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-NVIDIA\n'\
> /etc/zypp/repos.d/cuda.repo

RUN NVIDIA_GPGKEY_SUM=d1be581509378368edeec8c1eb2958702feedf3bc3d17011adbf24efacce4ab5 && \
curl -fsSL https://developer.download.nvidia.com/compute/cuda/repos/opensuse15/x86_64/7fa2af80.pub | sed '/^Version/d' > /etc/pki/rpm-gpg/RPM-GPG-KEY-NVIDIA && \
    echo "$NVIDIA_GPGKEY_SUM  /etc/pki/rpm-gpg/RPM-GPG-KEY-NVIDIA" | sha256sum -c --strict - && rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-NVIDIA

# For libraries in the cuda-compat-* package: https://docs.nvidia.com/cuda/eula/index.html#attachment-a
RUN zypper -n install -y \
    cuda-cudart-$CUDA_PKG_VERSION \
    cuda-compat-$CUDA_PKG_VERSION \
    && \
    ln -s cuda-$CUDA_PKG_VERSION /usr/local/cuda && \
    zypper clean -a;\
    ldconfig

ENV LIBRARY_PATH /usr/local/cuda-${CUDA_VERSION}/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
ENV PATH /usr/local/cuda-${CUDA_VERSION}/bin:/usr/local/cuda-${CUDA_VERSION}/NsightCompute-2019.1${PATH:+:${PATH}}
RUN echo "/usr/local/nvidia/lib" >> /etc/ld.so.conf.d/nvidia.conf && \
    echo "/usr/local/nvidia/lib64" >> /etc/ld.so.conf.d/nvidia.conf

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES compute,utility
ENV NVIDIA_REQUIRE_CUDA "cuda>=10.0 brand=tesla,driver>=384,driver<385 brand=tesla,driver>=410,driver<411"