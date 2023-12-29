[Documentation](https://spark.apache.org/docs/latest/ml-pipeline.html#main-concepts-in-pipelines)
- - -
Key concepts:
- **DataFrame:** This ML API uses `DataFrame` from Spark SQL as an ML dataset, which can hold a variety of data types (text, feature vectors, true labels, and predictions).
- **Transformer:** an algorithm which can transform one `DataFrame` into another `DataFrame`. 
	- A ML **model** is a `Transformer` which transforms a `DataFrame` with features into a `DataFrame` with predictions.
- **Estimator:** an algorithm which trains on a `DataFrame` to produce a `Transformer`. 
	- `LogisticRegression` is an `Estimator`, and calling `fit()` trains a `LogisticRegressionModel`, which is a `Model` and hence a `Transformer`.
- **Pipeline:** A `Pipeline` chains multiple `Transformers` and `Estimators` together to specify an ML workflow.
	- A `pipeline`  is essentially an `estimator`, because it has a `fit()` function.
	- When `pipeline.fit()` is called, it transform the original data via multiple transformations, then produce a fitted model (with the fitted weights).
	- The output of `pipeline.fit()` is a `PipelineModel`, which is a `transformer`. We can transform any `df` and produce the predictions using this pipeline model.

## Code example


```python
from pyspark.ml import Pipeline
from pyspark.ml.classification import LogisticRegression
from pyspark.ml.feature import HashingTF, Tokenizer

# Prepare training documents from a list of (id, text, label) tuples.
training = spark.createDataFrame([
    (0, "a b c d e spark", 1.0),
    (1, "b d", 0.0),
    (2, "spark f g h", 1.0),
    (3, "hadoop mapreduce", 0.0)
], ["id", "text", "label"])

# Configure an ML pipeline, which consists of [tokenizer, hashingTF, and lr].
tokenizer = Tokenizer(inputCol="text", outputCol="words")
hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
lr = LogisticRegression(maxIter=10, regParam=0.001)
pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

# Fit the pipeline to training documents.
model = pipeline.fit(training)

# Prepare test documents, which are unlabeled (id, text) tuples.
test = spark.createDataFrame([
    (4, "spark i j k"),
    (5, "l m n"),
    (6, "spark hadoop spark"),
    (7, "apache hadoop")
], ["id", "text"])

# Make predictions on test documents and print columns of interest.
prediction = model.transform(test)
selected = prediction.select("id", "text", "probability", "prediction")
for row in selected.collect():
    rid, text, prob, prediction = row
    print(
        "(%d, %s) --> prob=%s, prediction=%f" % (
            rid, text, str(prob), prediction   
        )
    )
```