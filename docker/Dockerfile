FROM tensorflow/tensorflow:1.13.1-gpu-jupyter

ENV DEBIAN_FRONTEND=noninteractive

# Linuxパッケージのインストール
RUN apt-get update && apt-get install -y \
    git \
    autoconf \
    tmux \
    vim \
    wget \
    cmake \
    byobu \
    language-pack-ja \
    unzip \
    nscd \
    graphviz \
    libgtk2.0-dev \
    libjpeg-dev \
    libpng-dev \
    libtiff-dev \
    protobuf-compiler \
    python-tk \
    python-pil \
    python-lxml \
    python-opengl \
    xvfb \
    ffmpeg  \
    python-pip \
    python3-pip \
    && apt-get -y clean all \
    && rm -rf /var/lib/apt/lists/*

# 言語設定
RUN locale-gen ja_JP.UTF-8
ENV LANGUAGE ja_JP:en
ENV LC_ALL ja_JP.UTF-8
ENV LANG ja_JP.UTF-8
RUN update-locale LANG=$LANG

# Pythonライブラリのインストール
RUN pip3 install --upgrade pip
RUN pip3 install torch==1.5.0+cu101 torchvision==0.6.0+cu101 -f https://download.pytorch.org/whl/torch_stable.html
COPY requirements.txt /tmp/
RUN pip install -r /tmp/requirements.txt
COPY . /tmp/

# pybullet-gymのインストール
RUN git clone https://github.com/benelot/pybullet-gym
RUN cd pybullet-gym \
&& git checkout 55eaa0defca7f4ae382963885a334c952133829d \
&& pip install -e .

# Tensorboardのポート番号
# EXPOSE 6006

# Jupyter Notebookのポート番号
EXPOSE 8888
