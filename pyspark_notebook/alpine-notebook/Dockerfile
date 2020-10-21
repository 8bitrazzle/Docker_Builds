FROM python:3-alpine3.12

ARG SPARK_VER=3.0.0

#install jupyter and library dependencies
RUN apk add --no-cache \
	bash \
	git \
	vim \
	openjdk8-jre \
	gcc \
	gfortran \
	build-base \
	freetype-dev \ 
	libpng-dev \
	openblas-dev \
	jpeg-dev \
	zlib-dev \
	libffi-dev	

#install jupyter and common libraries and their dependencies
RUN pip3 --no-cache-dir install \
	jupyter \
	jupyterlab \
	wheel \
	numpy \
	pandas \
	matplotlib 

#install pyspark
RUN pip3 --no-cache-dir install pyspark==$SPARK_VER

#required spark environment setup
ENV SPARK_HOME=/usr/local/spark
ENV PYSPARK_PYTHON=python3
ENV PYSPARK_DRIVER_PYTHON=python3
ENV PYTHONPATH=/usr/local/spark/python:/usr/local/spark/python/lib/py4j-0.10.7-src.zip
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/spark/bin

ENV SHELL=/bin/bash

EXPOSE 8888

RUN mkdir /notebooks
WORKDIR /notebooks

CMD /bin/bash -c "jupyter lab --ip=0.0.0.0 --port=8888 --no-browser --notebook-dir=/notebooks --allow-root"
	
