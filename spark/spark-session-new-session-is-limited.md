SparkSession.newSession is limited
===========

`pyspark.sql.SparkSession.newSession` does not actually allow you to create a new Spark context (as the name might suggest). 

It merely does this:

> Returns a new SQLContext as new session, that has separate SQLConf, registered temporary views and UDFs, but shared SparkContext and table cache.

As per [the docs](https://spark.apache.org/docs/latest/api/python/pyspark.sql.html).

Too many assumptions led to me thinking that a piece of code I reviewed was actually changing Spark's (-on-YARN's) resource request on the fly: it was calling `SparkSession.builder.conf(...).getOrCreate().newInstance()` with twice, with _different_ executor settings the second time (since the second task it did was heavier). However, at least in the YARN case, this was basically a no-op since the SparkContext remained unchanged and it kept the initial executor configuration.