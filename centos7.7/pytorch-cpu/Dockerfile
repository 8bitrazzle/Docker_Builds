FROM centos:7.7.1908

ENV PYTHON_VERSION 3.7
ENV CONDA_ENV_NAME jupyterlab

RUN yum update -y && yum install -y \
    wget \
    libSM \
    libXrender \
    libXext \
    curl \
    git  
         
RUN curl -sSL http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -o /tmp/miniconda.sh && \
    bash /tmp/miniconda.sh -bfp /usr/local && \
    rm -rf /tmp/miniconda.sh

RUN conda update -y conda && \
    conda create -n ${CONDA_ENV_NAME} python=${PYTHON_VERSION}
ENV PATH /opt/conda/envs/${CONDA_ENV_NAME}/bin:$PATH
RUN echo "source activate ${CONDA_ENV_NAME}" > ~/.bashrc

RUN /bin/bash -c "source ~/.bashrc && conda install -q -y jupyterlab && jupyter serverextension enable --py jupyterlab"

RUN /bin/bash -c "source ~/.bashrc && conda install -q -y nodejs && \
    jupyter labextension install @jupyterlab/git && \
    pip --no-cache-dir install jupyterlab-git && \
    jupyter serverextension enable --py jupyterlab_git"

RUN /bin/bash -c "source ~/.bashrc && \
    jupyter labextension install @jupyterlab/github && \
    pip --no-cache-dir install jupyterlab_github && \
    jupyter serverextension enable --sys-prefix jupyterlab_github"

RUN /bin/bash -c "source ~/.bashrc && pip --no-cache-dir install \
    torch==1.3.1+cpu torchvision==0.4.2+cpu -f https://download.pytorch.org/whl/torch_stable.html \
    matplotlib \
    opencv-python \
    cython \
    numpy \
    pandas \
    pillow==6.2.0"

RUN yum clean all && \
    rm -rf /var/lib/apt/lists/*
RUN conda clean --all --yes

EXPOSE 30300

RUN mkdir /notebook
WORKDIR /notebook

CMD /bin/bash -c "source ~/.bashrc && jupyter lab --ip=0.0.0.0 --port=30300 --no-browser --notebook-dir=/notebook --allow-root"
