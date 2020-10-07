PySpark Submit Entire Conda Environment
=======================================

When working on large enterprise Spark / Hadoop clusters, you are probably not control of the Python interpreter on the worker nodes. Luckily, it's possible - and quite easy - to include entire conda environments in your spark-submit. Here's how to do it with YARN (but probably also works with standalone Spark).

# 1. Create conda env

	conda create --name py37-spark python=3.7

# 2. Install dependencies
At the very least, install pyspark. Use the exact same version as running on the cluster.

	conda activate py37-spark
	conda install pyspark==2.4.6

# 3. Use conda pack to create a tarball

	conda install -c anaconda conda-pack   # If not installed already
	conda pack -n py37-spark

This will create a tarball `py37-spark.tar.gz`.

# 4. Example YARN spark-submit with deploy-mode client

export PYSPARK_DRIVER_PYTHON="`which python`" # Assumes env currently active 
export PYSPARK_PYTHON=conda-env/bin/python

spark-submit \
  --archives "py37-spark.tgz#conda-env" \
  --master yarn \
  --deploy-mode client \
  file.py

# 5. Example YARN spark-submit with deploy-mode cluster

spark-submit \
  --conf spark.yarn.appMasterEnv.PYSPARK_DRIVER_PYTHON=conda-env/bin/python \
  --conf spark.yarn.appMasterEnv.PYSPARK_PYTHON=conda-env/bin/python \
  --archives "py37-spark.tgz#conda-env" \
  --master yarn \
  --deploy-mode cluster \
  file.py
