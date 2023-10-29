Datasets are similar to [[DataFrame]], but are **type-safe.** Not applicable to R and Python since they are dynamically typed.


```Scala

case class Flight(DEST_COUNTRY_NAME: String, ORIGIN_COUNTRY_NAME: String, count: BigInt) 

val flightsDF = spark.read.parquet("/mnt/defg/flight-data/parquet/2010- summary.parquet/") 

val flights = flightsDF.as[Flight] 

flights.collect()
```