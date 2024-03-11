FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

ARG USERNAME=tomoya-s

RUN apt-get -y update
RUN apt install -y git sudo cmake
RUN apt install -y curl emacs nano wget g++ pkg-config
RUN apt install -y libglib2.0-dev kmod nvme-cli
RUN apt install -y python3-numpy bc numactl

RUN useradd -m $USERNAME
RUN gpasswd -a $USERNAME sudo
RUN echo "${USERNAME}:hogehoge" | chpasswd

RUN echo "$USERNAME ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

USER $USERNAME
RUN git config --global user.email "t3suzuki@ucsd.edu"
RUN git config --global user.name "Tomoya Suzuki"


USER $USERNAME
WORKDIR /home/$USERNAME/

COPY dotemacs /home/$USERNAME/.emacs

RUN git clone https://github.com/Thesys-lab/sosp23-s3fifo.git
#RUN git clone https://github.com/t3suzuki/sosp23-s3fifo.git
WORKDIR /home/$USERNAME/sosp23-s3fifo/libCacheSim/scripts
RUN bash install_dependency.sh
RUN bash install_libcachesim.sh

WORKDIR /home/$USERNAME/sosp23-s3fifo
RUN git clone https://github.com/Thesys-lab/cachelib-sosp23
#RUN git clone https://github.com/t3suzuki/cachelib-sosp23
RUN ln -sf cachelib-sosp23 cachelib
#RUN python3 libCacheSim/scripts/data_gen.py -m 1000000 -n 100000000 --alpha 1.0 --bin-output cachelib/mybench/zipf1.0_1_100.oracleGeneral.bin
RUN python3 libCacheSim/scripts/data_gen.py -m 1000000 -n 10000000 --obj-size 16 --alpha 0.4 --bin-output cachelib/mybench/zipf0.4_1M_10M.oracleGeneral.bin
RUN python3 libCacheSim/scripts/data_gen.py -m 1000000 -n 10000000 --obj-size 16 --alpha 0.99 --bin-output cachelib/mybench/zipf0.99_1M_10M.oracleGeneral.bin

WORKDIR /home/$USERNAME/sosp23-s3fifo/cachelib/mybench
RUN sudo apt install -y apt apt-utils


#RUN bash turboboost.sh disable

RUN sed -i -e 's/clear//' build.sh
RUN bash ./build.sh

# RUN make
