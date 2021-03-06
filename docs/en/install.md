---
layout: article
title: Installation
permalink: /docs/en/install
key: docs-install
modify_date: "2020-05-26"
---

## Spark NLP Cheat Sheet

```bash
# Install Spark NLP from PyPI
$pip install spark-nlp==2.5.2

# Install Spark NLP from Anacodna/Conda
conda install -c johnsnowlabs spark-nlp

# Load Spark NLP with Spark Shell
spark-shell --packages com.johnsnowlabs.nlp:spark-nlp_2.11:2.5.2

# Load Spark NLP with PySpark
pyspark --packages com.johnsnowlabs.nlp:spark-nlp_2.11:2.5.2

# Load Spark NLP with Spark Submit
spark-submit --packages com.johnsnowlabs.nlp:spark-nlp_2.11:2.5.2

# Load Spark NLP as external JAR after comiling and bulding Spark NLP by `sbt assembly`
spark-shell --jar spark-nlp-assembly-2.5.2
```

## Python

### Quick Install

Let's create a new Conda environment to manage all the dependencies there. You can use Python Virtual Environment if you prefer or not have any enviroment.

```bash
$ java -version
# should be Java 8 (Oracle or OpenJDK)
$ conda create -n sparknlp python=3.6 -y
$ conda activate sparknlp
$ pip install spark-nlp==2.5.2 pyspark==2.4.4
```

Of course you will need to have jupyter installed in your system:

```bash
pip install jupyter
```

Now you should be ready to create a jupyter notebook running from terminal:

```bash
jupyter notebook
```

### Start Spark NLP Session from python

If you need to manually start SparkSession because you have other configuraations and `sparknlp.start()` is not including them, you can manually start the SparkSession:

```python
spark = SparkSession.builder \
    .appName("Spark NLP")\
    .master("local[4]")\
    .config("spark.driver.memory","16G")\
    .config("spark.driver.maxResultSize", "2G") \
    .config("spark.jars.packages", "com.johnsnowlabs.nlp:spark-nlp_2.11:2.5.2")\
    .config("spark.kryoserializer.buffer.max", "1000M")\
    .getOrCreate()
```

## Scala and Java

Our package is deployed to maven central. In order to add this package
as a dependency in your application:

### Maven

```xml
<!-- https://mvnrepository.com/artifact/com.johnsnowlabs.nlp/spark-nlp -->
<dependency>
    <groupId>com.johnsnowlabs.nlp</groupId>
    <artifactId>spark-nlp_2.11</artifactId>
    <version>2.5.2</version>
</dependency>
```

and

```xml
<!-- https://mvnrepository.com/artifact/com.johnsnowlabs.nlp/spark-nlp-gpu -->
<dependency>
    <groupId>com.johnsnowlabs.nlp</groupId>
    <artifactId>spark-nlp-gpu_2.11</artifactId>
    <version>2.5.2</version>
</dependency>
```

### SBT

```bash
// https://mvnrepository.com/artifact/com.johnsnowlabs.nlp/spark-nlp
libraryDependencies += "com.johnsnowlabs.nlp" %% "spark-nlp" % "2.5.2"
```

and

```bash
// https://mvnrepository.com/artifact/com.johnsnowlabs.nlp/spark-nlp-gpu
libraryDependencies += "com.johnsnowlabs.nlp" %% "spark-nlp-gpu" % "2.5.2"
```

Maven Central: [https://mvnrepository.com/artifact/com.johnsnowlabs.nlp](https://mvnrepository.com/artifact/com.johnsnowlabs.nlp)

## Databricks

### Databricks Support

Spark NLP 2.5.2 has been tested and is compatible with the following runtimes:

* 6.2
* 6.2 ML
* 6.3
* 6.3 ML
* 6.4
* 6.4 ML
* 6.5
* 6.5 ML

### Install Spark NLP on Databricks

1. Create a cluster if you don't have one already

2. On a new cluster or existing one you need to add the following to the `Aadvanced Options -> Spark` tab:

```bash
spark.kryoserializer.buffer.max 1000M
spark.serializer org.apache.spark.serializer.KryoSerializer
```

3. In `Libraries` tab inside your cluster you need to follow these steps:

    3.1. Insatll New -> PyPI -> `spark-nlp` -> Install

    3.2. Install New -> Maven -> Coordinates -> `com.johnsnowlabs.nlp:spark-nlp_2.11:2.5.2` -> Install

4. Now you can attach your notebook to the cluster and use Spark NLP!

### Databricks Notebooks

You can view all the Databricks notebooks from this address:

[https://johnsnowlabs.github.io/spark-nlp-workshop/databricks/index.html](https://johnsnowlabs.github.io/spark-nlp-workshop/databricks/index.html)

Note: You can import these notebooks by using their URLs.
