Import SparkSession: Import the SparkSession class from the PySpark library.

Create Spark Session: Build a Spark session with various configurations such as the application name, master URL (local mode with 2 cores), executor memory, dynamic allocation enabled, broadcast join threshold, serializer, garbage collection settings, checkpointing, shuffle partitions, storage fraction, and Hive configurations.

## Read CSV file with options
csv_df = spark.read.option("header", "true").csv("path/to/csvfile")
Read CSV File: Use the spark.read.option method to read a CSV file into a DataFrame (csv_df). The option "header" is set to "true" to consider the first row as the header.

## Read Parquet file
parquet_df = spark.read.parquet("path/to/parquetfile")
Read Parquet File: Read a Parquet file into another DataFrame (parquet_df).

## Interact with Hive using Spark SQL
spark.sql("SHOW DATABASES")
Interact with Hive: Execute a Spark SQL query to show the available databases in Hive.

## Broadcast smaller tables during joins
spark.conf.set("spark.sql.autoBroadcastJoinThreshold", "10m")
Broadcast Threshold for Joins: Set the threshold for automatically broadcasting smaller tables during joins to improve performance.

## Configure compression codec for Parquet files
spark.conf.set("spark.sql.parquet.compression.codec", "snappy")
Compression for Parquet Files: Set the compression codec (in this case, "snappy") for Parquet files.

## Enable dynamic allocation for adjusting executors dynamically
spark.conf.set("spark.dynamicAllocation.enabled", "true")
Dynamic Allocation: Enable dynamic allocation to adjust the number of executors dynamically based on workload.

## Configure Hive metastore URIs and warehouse directory
spark.conf.set("spark.sql.warehouse.dir", "/user/hive/warehouse")
spark.conf.set("hive.metastore.uris", "thrift://localhost:9083")
Hive Metastore Configuration: Configure Hive metastore URIs and the warehouse directory.

## Set serializer for optimizing data serialization and deserialization
spark.conf.set("spark.serializer", "org.apache.spark.serializer.KryoSerializer")
Serializer Configuration: Set the serializer to optimize data serialization and deserialization using KryoSerializer.

## Tune garbage collection settings for Spark executors
spark.conf.set("spark.executor.extraJavaOptions", "-XX:+UseG1GC")
Garbage Collection Tuning: Tune garbage collection settings for Spark executors using the G1 garbage collector.

## Enable automatic checkpointing for fault tolerance
spark.conf.set("spark.checkpoint.auto", "true")
Checkpointing Configuration: Enable automatic checkpointing to truncate lineage and improve fault tolerance.
 
## Set the number of partitions to use when shuffling data
spark.conf.set("spark.sql.shuffle.partitions", "200")
Shuffle Partitions Configuration: Set the number of partitions to use when shuffling data.
 
## Configure Hive properties for Spark SQL
spark.sql("SET spark.sql.hive.convertMetastoreOrc=false")
Hive Properties Configuration: Set specific Hive properties using a Spark SQL query.
 
## Set the portion of the executor's memory dedicated to Spark storage
spark.conf.set("spark.memory.storageFraction", "0.4")
Memory Fraction for Storage: Set the portion of the executor's memory dedicated to Spark storage.
 
## Run SQL queries on DataFrames
csv_df.createOrReplaceTempView("csv_table")
result_df = spark.sql("SELECT * FROM csv_table WHERE age > 25")
result_df.show()
Run SQL Queries: Create a temporary view from the CSV DataFrame and execute a SQL query on it, showing the results.
 
## Stop the Spark session
spark.stop()
Stop Spark Session: Terminate the Spark session to release resources.
This comprehensive script covers Spark configurations, file handling, Hive integration, SQL queries, and more. Adjustments can be made based on your specific use case and cluster settings.

from pyspark.sql import SparkSession

# Create a Spark session with master URL and application name
spark = SparkSession.builder \
    .appName("MySparkApp") \
    .master("local[2]") \
    .config("spark.executor.memory", "2g") \
    .config("spark.executor.cores", "4") \
    .config("spark.dynamicAllocation.enabled", "true") \
    .config("spark.sql.autoBroadcastJoinThreshold", "10m") \
    .config("spark.serializer", "org.apache.spark.serializer.KryoSerializer") \
    .config("spark.executor.extraJavaOptions", "-XX:+UseG1GC") \
    .config("spark.checkpoint.auto", "true") \
    .config("spark.sql.shuffle.partitions", "200") \
    .config("spark.memory.storageFraction", "0.4") \
    .config("spark.sql.hive.convertMetastoreOrc", "false") \
    .getOrCreate()

### Read CSV file with options
csv_df = spark.read.option("header", "true").csv("path/to/csvfile")

### Read Parquet file
parquet_df = spark.read.parquet("path/to/parquetfile")

### Interact with Hive using Spark SQL
spark.sql("SHOW DATABASES")

### Broadcast smaller tables during joins
spark.conf.set("spark.sql.autoBroadcastJoinThreshold", "10m")

### Configure compression codec for Parquet files
spark.conf.set("spark.sql.parquet.compression.codec", "snappy")

### Enable dynamic allocation for adjusting executors dynamically
spark.conf.set("spark.dynamicAllocation.enabled", "true")

### Configure Hive metastore URIs and warehouse directory
spark.conf.set("spark.sql.warehouse.dir", "/user/hive/warehouse")
spark.conf.set("hive.metastore.uris", "thrift://localhost:9083")

### Set threshold for broadcasting smaller tables during joins
spark.conf.set("spark.sql.autoBroadcastJoinThreshold", "10m")

### Set serializer for optimizing data serialization and deserialization
spark.conf.set("spark.serializer", "org.apache.spark.serializer.KryoSerializer")

### Tune garbage collection settings for Spark executors
spark.conf.set("spark.executor.extraJavaOptions", "-XX:+UseG1GC")

### Enable automatic checkpointing for fault tolerance
spark.conf.set("spark.checkpoint.auto", "true")

### Set the number of partitions to use when shuffling data
spark.conf.set("spark.sql.shuffle.partitions", "200")

### Configure Hive properties for Spark SQL
spark.sql("SET spark.sql.hive.convertMetastoreOrc=false")

### Set the portion of the executor's memory dedicated to Spark storage
spark.conf.set("spark.memory.storageFraction", "0.4")

### Run SQL queries on DataFrames
csv_df.createOrReplaceTempView("csv_table")
result_df = spark.sql("SELECT * FROM csv_table WHERE age > 25")
result_df.show()

### Stop the Spark session
spark.stop()"""
