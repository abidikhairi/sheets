# Apache Spark

### submitting spark jobs

`spark-submit --jars path/to/additional/jarfile.jar --class fully.qualified.class.Name path/to/job.jar` 

### read from JDBC source
database Driver: `org.postgresql:postgresql:42.2.8`

```scala
val df = spark.read
	.format("jdbc")
	.option("url", "jdbc:postgresql://host:port/dbname")
	.option("dbtable", "tablename")
	.option("user", "demo")
	.option("password", "demo")
	.load();
```

### _lag_ over non null column

```scala
val window = Window.partitionBy("col1", "col2").orderBy("DateCol")

val result = df.withColumn("t1", when(col("testCol") === 0,
        last(when(col("testCol") !== 0, col("targetCol")), ignoreNulls= true).over(window)))

    .withColumn("t2", when(col("testCol") > 0.0,
        lag(col("targetCol"), 1, "defaultVal").over(window))
        .otherwise(col("t1")))
    
    .withColumn("PrevOrderDate", when(col("testCol") > 0.0 && col("t1").isNull,
        lag(col("t2"), 1, "defaultVal").over(window))
        .otherwise(col("t2")))
```

### parse date column

```scala
val format = "yyyy-MM-dd"

val result = df.withColumn("newDateCol", to_date(col("dateCol"), format))
```
