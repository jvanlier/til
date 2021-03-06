`backfill` cli command: `--ignore_dependencies` breaks `depends_on_past`
======

In Airflow 1.10.14, the `airflow backfill` command has an argument called `--ignore_dependencies` that has some weird side effects.

According to the docs, it does this:

> Skip upstream tasks, run only the tasks matching the regexp. Only works in conjunction with task_regex

However, when used on a task that has `depends_on_past=True`, it makes the backfill command not honor it: it will just run all tasks in parallel. I guess in a way they are upstream tasks, but I can't think of any scenario where this is desired behavior.

This means that you are forced to run all upstream tasks when you want to backfill a task with `depends_on_past=True` properly, unfortunately.

