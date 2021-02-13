Changing Spark resources only possible with `spark.stop()` 
===========

When working with Spark, sometimes you only need few executors and sometimes you need many.

As hinted at in [spark-session-new-session-does-not-do-what-you-think-it-does](spark-session-new-session-does-not-do-what-you-think-it-does.md), it's not possible to change resources for a running SparkSession with `newInstance()`.

This further substantiates that claim:
      
```
print(spark.conf.isModifiable("spark.executor.cores"))
print(spark.conf.isModifiable("spark.executor.memory"))
print(spark.conf.isModifiable("spark.executor.instances"))
print(spark.conf.isModifiable("spark.dynamicAllocation.maxExecutors"))
print(spark.conf.isModifiable("spark.default.parallelism"))
```

This all returns `False`. (However, `spark.sql.*` stuff such as `spark.sql.shuffle.partitions` does return `True`.)

The only way to change executor resources, as far as I know, is to `spark.stop()` and create it again with 
`SparkSession.builder.getOrCreate()`.
But beware: this does not work in `deploy-mode cluster`: [spark-stop-and-restart-only-possible-in-deploy-mode-client.md](spark-stop-and-restart-only-possible-in-deploy-mode-client.md.md)

N.b.: this was only tested with Spark-on-YARN, things might be different in standalone mode.