# Pyenv with optimizations

Pyenv compiles Python from source.
When doing so, it does not use optimizations by default.

[The docs state][docs-maximum-performance]:

> Building CPython with --enable-optimizations will result in a faster interpreter at the cost of significantly longer build times. Most notably, this enables PGO (profile guided optimization). While your mileage may vary, it is common for performance improvement from this to be in the ballpark of 30%.

Seems worth it!

```sh
export PYTHON_CONFIGURE_OPTS='--enable-optimizations --with-lto' PYTHON_CFLAGS='-march=native -mtune=native'
export PROFILE_TASK='-m test.regrtest --pgo -j0'

pyenv install --verbose 3.12.7
```

[docs-maximum-performance]: https://github.com/pyenv/pyenv/blob/master/plugins/python-build/README.md#building-for-maximum-performance


