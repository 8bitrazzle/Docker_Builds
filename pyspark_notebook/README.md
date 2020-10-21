# Building spark worker containers for the notebook drivers
1. Grab the latest version of spark and unpack (ensure to choose correct hadoop version as well if needed)
   * wget -qO- http://mirrors.gigenet.com/apache/spark/spark-x.x.x/spark-x.x.x-bin-hadoop2.7.tgz | tar -zxvf -

2. change into the new spark-x.x.x-bin-hadoop2.7 directory and build the spark container with python
   * ./bin/docker-image-tool.sh -r pyspark -t v3.0.1 -p kubernetes/dockerfiles/spark/bindings/python/Dockerfile build
