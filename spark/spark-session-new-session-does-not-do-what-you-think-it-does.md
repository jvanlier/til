SparkSession.newSession does not do what you think it does
===========

`pyspark.sql.SparkSession.newSession` does not actually allow you to create a new Spark *Context* (as the name might suggest). 

It merely does this:

> Returns a new SQLContext as new session, that has separate SQLConf, registered temporary views and UDFs, but shared SparkContext and table cache.

As per [the docs](https://spark.apache.org/docs/latest/api/python/pyspark.sql.html).

Too many assumptions led to me thinking that a piece of code I reviewed was actually changing Spark's resource request on the fly: it was calling `SparkSession.builder.conf(...).getOrCreate().newInstance()` after having done some Spark work, the second time with _different_ executor settings. However, this was basically a no-op since there were no SQLConf-specific settings, temporary views or UDFs. The SparkContext remained unchanged and it kept the initial executor configuration (verified by checking the Spark UI).

N.b.: this was only tested with Spark-on-YARN, things might be different in standalone mode.