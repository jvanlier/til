Set Driver Memory in YARN deploy-mode cluster
=============================================

Setting driver memory in YARN `deploy-mode cluster` is slightly weird, in that it cannot be done using `SparkSession.builder.config`. 
By the time your submitted code can run this, the container is already created. It's too late to make changes.

There's two command line flags that work:

	`--driver-memory 8g`
        `--conf spark.driver.memory=8g`

They both seem to work fine, I don't think there's any difference between them.

N.b.: I mention YARN specifically because I have only tested this with YARN and not with other cluster managers.
