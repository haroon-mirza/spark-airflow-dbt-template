FROM apache/airflow:2.9.2
# Using uv for faster pip installs
RUN pip install uv

# Copy and install python requirements
COPY requirements.txt $AIRFLOW_HOME
RUN uv pip install -r $AIRFLOW_HOME/requirements.txt

# Switch to root user to install system-level packages
USER root

# Install JDK for spark
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    default-jdk

# Download and install spark
RUN curl https://archive.apache.org/dist/spark/spark-3.5.1/spark-3.5.1-bin-hadoop3.tgz -o spark-3.5.1-bin-hadoop3.tgz && \
    chmod 755 spark-3.5.1-bin-hadoop3.tgz && \
    mkdir -p /opt/spark && \
    tar xvzf spark-3.5.1-bin-hadoop3.tgz --directory /opt/spark --strip-components=1 && \
    rm spark-3.5.1-bin-hadoop3.tgz

# Set environment variables for Java and Spark
ENV JAVA_HOME='/usr/lib/jvm/java-17-openjdk-amd64'
ENV PATH=$PATH:$JAVA_HOME/bin
ENV SPARK_HOME='/opt/spark'
ENV PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin