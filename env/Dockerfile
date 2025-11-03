# Adding NCCL tests on top of nvidia/pytorch container
FROM nvcr.io/nvidia/pytorch:25.03-py3

ENV NCCL_TESTS_TAG=v2.16.4

# 90 is the gencode for H100
RUN mkdir /tmp/nccltests \
    && cd /tmp/nccltests \
    && git clone -b ${NCCL_TESTS_TAG} https://github.com/NVIDIA/nccl-tests.git \
    && cd nccl-tests \
    && make \
        MPI=1 MPI_HOME=/opt/hpcx/ompi \
        NVCC_GENCODE="-gencode=arch=compute_90,code=sm_90" \
        CUDA_HOME=/usr/local/cuda \
    && cp ./build/* /usr/local/bin \
    && rm -rf /tmp/nccltests
