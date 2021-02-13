`spark.stop()` and restart only possible in `deploy-mode client`
========
 In my current project, the scientists develop with `deploy-mode client` and we (engineers) run the same code in production with `deploy-mode cluster`. 
 
 In order to better tune Spark settings to workloads, a pattern such as `spark.stop()` followed by `SparkSession.builder.config(...).getOrCreate()` could easily appear in a Jupyter Notebook or a `.py` script to re-configure the Spark settings.
 
 This works well in `deploy-mode client`: the Python kernel on the driver stays alive, it creates a new SparkSession (with SparkContext) and you get a new YARN application id.

As it turns out, this does _not_ work with `deploy-mode cluster`, probably because it deallocates the container that the driver lives in. There is no choice but to re-submit.

N.b.: this was only tested with Spark-on-YARN, things might be different in standalone mode.