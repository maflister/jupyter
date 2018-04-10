BootStrap: docker
From: ubuntu:latest

%help
    This container runs a jupyter notebook on a compute node.

%labels
    Maintainer Matthew Flister
    Version v18.04

%post
    mkdir -p /scratch/global /scratch/local /rcc/stor1/refdata /rcc/stor1/projects /rcc/stor1/depts
    apt-get update
    apt-get -y install python3 python3-pip python python-pip
    pip install jupyter
    pip3 install jupyter

