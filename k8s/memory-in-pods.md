# Memory in pods

The memory limits of pods in k8s are enforced on `cgroup` level.

This means that processes actually get killed when the pod exceeds the requested memory, even though it may seem like more memory is available (if you look in the wrong place). 

## Don't run `free`, `top` etc to determine how much memory you can use
The kernel is shared between different pods, and `free` and `top` simply query the host OS.

If you go by `free` and think "great, my app can use all of that", well, you'll be in for a surprise when your process gets killed once it exceeds the limit.

## Make your app aware
In the case of Java, Go, probably also other languages, there's flags you can pass at runtime to detect the cgroup settings and treat those as the actual limits of the workload.

There’s a special file called `/sys/fs/cgroup/memory/memory.limit_in_bytes` that you can read at startup.
