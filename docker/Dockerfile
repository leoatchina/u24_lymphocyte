FROM nvidia/cuda:8.0-cudnn5-devel 
MAINTAINER  leoatchina
COPY docker/requirements.txt /root/requirements.txt
COPY docker/run_*.sh /usr/bin/ 
COPY docker/theanorc /root/.theanorc
RUN	chmod 0755 /usr/bin/run_*.sh && apt-get -y update && \
    apt-get -y install libfontconfig1 libxrender1 libxtst6 wget curl git tmux htop


ENV	PATH=/root/miniconda2/bin:$PATH
RUN	\
    cd /tmp && \
    curl https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda2-4.5.1-Linux-x86_64.sh -o Miniconda2-Linux-x86_64.sh && \
    sh Miniconda2-Linux-x86_64.sh -b && \
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ && \
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/ && \
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/ && \
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/ && \
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/ && \
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/menpo/ && \
    conda config --set show_channel_urls yes && \
    pip install --upgrade pip && \
    conda clean -a -y && \
    rm -rf /tmp/*
                 
RUN conda install \
    -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge \
    -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda --yes --file /root/requirements.txt && \
    conda clean -a -y && \
    rm -rf /tmp/*
RUN conda install -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge --yes libiconv pygpu && \
    conda clean -a -y && \
    rm -rf /tmp/*

RUN \
    pip install cython msgpack openslide-python theano==0.9.0 && \
    pip install --upgrade https://github.com/Lasagne/Lasagne/archive/master.zip && \
    rm -rf /root/.cache/pip/* /tmp/*


CMD ["/bin/bash"]
