BootStrap: docker
From: ubuntu:latest

%help
    This container runs a Jupyter Notebook on a compute node.

%labels
    Maintainer Matthew Flister
    Version v18.04

%setup
    install -Dv \
    kernels/python2/tensorflow17.json \
    ${SINGULARITY_ROOTFS}/usr/share/jupyter/kernels/python2/TensorFlow17/kernel.json
    install -Dv \
    kernels/python2/tensorflow16.json \
    ${SINGULARITY_ROOTFS}/usr/share/jupyter/kernels/python2/TensorFlow16/kernel.json
    install -Dv \
    kernels/python2/tensorflow12.json \
    ${SINGULARITY_ROOTFS}/usr/share/jupyter/kernels/python2/TensorFlow12/kernel.json
    install -Dv \
    kernels/python3/tensorflow17.json \
    ${SINGULARITY_ROOTFS}/usr/share/jupyter/kernels/python3/TensorFlow17/kernel.json
    install -Dv \
    kernels/python3/tensorflow16.json \
    ${SINGULARITY_ROOTFS}/usr/share/jupyter/kernels/python3/TensorFlow16/kernel.json
    install -Dv \
    kernels/python3/tensorflow12.json \
    ${SINGULARITY_ROOTFS}/usr/share/jupyter/kernels/python3/TensorFlow12/kernel.json

%post
    # make mount points
    mkdir -p /scratch/global /scratch/local /rcc/stor1/refdata /rcc/stor1/projects /rcc/stor1/depts
    # install deps
    apt-get update
    apt-get -y install python3 python3-pip python python-pip
    apt-get clean
    #install python pkgs
    pip install --no-cache-dir --upgrade pip
    pip3 install --no-cache-dir --upgrade pip
    pip install jupyter ipykernel
    pip3 install jupyter ipykernel

