A DataFrame represents a **table of data**, similar to tables in SQL, or DataFrames in pandas.

It is a higher level inferface to [[Resilient Distributed Datasets|RDD]]. It is the recommended interface for working with Spark – they are easier to use than RDDs and almost all tasks can be done with them.


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
