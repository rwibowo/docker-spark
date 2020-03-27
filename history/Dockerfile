FROM bde2020/spark-base:2.4.5-hadoop2.7

LABEL maintainer="Gezim Sejdiu <g.sejdiu@gmail.com>, Giannis Mouchakis <gmouchakis@gmail.com>, Rio Wibowo <wibowo.rio@gmail.com>"

ENV SPARK_HOME=/spark

COPY entrypoint.sh /opt/
RUN chmod 777 -R /opt/entrypoint.sh

RUN apk add --no-cache tini

# Set up dependencies for Google Cloud Storage access.
RUN rm $SPARK_HOME/jars/guava-14.0.1.jar
ADD https://repo1.maven.org/maven2/com/google/guava/guava/23.0/guava-23.0.jar $SPARK_HOME/jars
# Add the connector jar needed to access Google Cloud Storage using the Hadoop FileSystem API.
ADD https://storage.googleapis.com/hadoop-lib/gcs/gcs-connector-latest-hadoop2.jar $SPARK_HOME/jars

# Add dependency for hadoop-aws
ADD https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk/1.7.4/aws-java-sdk-1.7.4.jar $SPARK_HOME/jars
# Add hadoop-aws to access Amazon S3
ADD https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-aws/2.7.5/hadoop-aws-2.7.5.jar $SPARK_HOME/jars

# Add dependency for hadoop-azure
ADD https://repo1.maven.org/maven2/com/microsoft/azure/azure-storage/2.0.0/azure-storage-2.0.0.jar $SPARK_HOME/jars
# Add hadoop-azure to access Azure Blob Storage
ADD https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-azure/2.7.3/hadoop-azure-2.7.3.jar $SPARK_HOME/jars

ENTRYPOINT ["/opt/entrypoint.sh"]