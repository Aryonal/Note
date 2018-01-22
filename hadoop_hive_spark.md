# Data Mining Utilities

about installations and configurations of Hadoop, pySpark, Hive

```sh
#make sure JDK 8 is installed
$ apt install openjdk-8-jdk
```

## Installation of Hadoop

```sh
#Before install
$ apt install ssh rsync
```

1. Download .tgz file from [Apache download mirrors](http://www.apache.org/dyn/closer.cgi/hadoop/common/)
2. unzip and mv to /path/to/hadoop
3. export HADOOP_HOME
4. set configurations at /path/to/hadoop/etc/hadoop/

excute
`
$ hadoop
`
to test.

## Installation of pySpark

1. Download .tgz file from [Download from Apache](http://spark.apache.org/downloads.html)
2. unzip and mv to /path/to/spark
3. export SPARK_HOME
4. echo `function snotebook()` to .bashrc (or .zshrc)
5. install jupyter using `pip install jupyter`

```sh
function snotebook ()
{
    #Spark path (based on your computer)
    SPARK_PATH='/opt/datamining/spark/'

    export PYSPARK_DRIVER_PYTHON="jupyter"
    export PYSPARK_DRIVER_PYTHON_OPTS="notebook"

	# For python 3 users, you have to add the line below or you will get an error
    #export PYSPARK_PYTHON=python3

    $SPARK_PATH/bin/pyspark --master local[2]
}
```

excute `$ $SPARK_HOME/bin/pyspark` to test

## Installation of Hive

1. Download .tgz file from [Apache download mirrors](http://www.apache.org/dyn/closer.cgi/hive/)
2. unzip and mv to /path/to/hive
3. export HIVE_HOME
