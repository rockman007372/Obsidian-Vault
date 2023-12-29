A DataFrame represents a **table of data**, similar to tables in SQL, or DataFrames in pandas.

It is a higher level inferface to [[Resilient Distributed Datasets|RDD]]. It is the **recommended interface** for working with Spark – they are easier to use than RDDs and almost all tasks can be done with them.

```python
flightData2015 = spark.read
	.option("inferSchema", "true")
	.option("header", "true")
	.csv("/mnt/defg/flight-data/csv/2015-summary.csv")

flightData2015
	.groupBy("DEST_COUNTRY_NAME")
	.sum("count")
	.withColumnRenamed("sum(count)", "destination_total") 
	.sort(desc("destination_total"))
	.limit(5)
	.collect()


# equivalent SQL code

flightData2015.createOrReplaceTempView("flight_data_2015") 

maxSql = spark.sql(
	""" 
	SELECT DEST_COUNTRY_NAME, sum(count) as destination_total 
	FROM flight_data_2015 
	GROUP BY DEST_COUNTRY_NAME 
	ORDER BY sum(count) DESC 
	LIMIT 5 
	"""
) 

maxSql.collect()

```

## Difference from [[Resilient Distributed Datasets|RDD]]

With RDD, you tell Sparks what to do. This leaves little room for optimization.

```python
# Create an RDD of tuples (name, age)
dataRDD = sc.parallelize([("Brooke", 20), ("Denny", 31), ("Jules", 30),("TD", 35), ("Brooke", 25)])

# Use map and reduceByKey transformations with their lambda
# expressions to aggregate and then compute average
agesRDD = (dataRDD
	.map(lambda x: (x[0], (x[1], 1)))
	.reduceByKey(lambda x, y: (x[0] + y[0], x[1] + y[1]))
	.map(lambda x: (x[0], x[1][0] / x[1][1])))
```

With Dataframe, you tell Sparks what you want to do. Spark does the optimization for you.

```python
# Create a DataFrame
data_df = spark.createDataFrame(
	[
		("Brooke", 20), 
		("Denny", 31), 
		("Jules", 30), 
		("TD", 35), 
		("Brooke", 25)
	], 
	["name", "age"]
)

# Group the same names together, aggregate their ages, and compute an average
avg_df = data_df.groupBy("name").agg(avg("age"))

# Show the results of the final execution
avg_df.show()
```

