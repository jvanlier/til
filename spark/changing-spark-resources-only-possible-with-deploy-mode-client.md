Changing Spark resources only possible with `deploy-mode client`
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

Ok, then `spark.stop()` and run `SparkSession.builder.getOrCreate()` again, right? "It works in my Notebook!". And in fact it does: it creates a new SparkSession with new new settings and you get a new YARN id.

As it turns out, this does _not_ work with `deploy-mode cluster`, probably because it deallocates the container that the driver lives in. In my current project, the scientists develop with `deploy-mode client` and we run the same code in production with `deploy-mode cluster`, so this is kind of a big deal.

N.b.: this was only tested with Spark-on-YARN, things might be different in standalone mode.