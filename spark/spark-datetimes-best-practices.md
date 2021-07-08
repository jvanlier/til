Spark Timestamps best practices
===============================

The `timestamp` data type in Spark is _not_ timezone aware. There are a few things in Spark that assume `timestamp`s are UTC:

- comparisons in PySpark with timezone-aware `datetime.datetime`s: `df.filter(col("timestamp") > pytz.timezone("Europe/Amsterdam").localize(datetime(2021, 7, 5, 12, 0, 0)))`. Spark actually does this correctly if the `timestamp` is in UTC! If the timestamp is naively in Europe/Amsterdam, however, you may get 4 hour differences in summer... silently!
- displays in the Databricks managed service: the data browser converts them to string representation with a timezone suffix, assuming they're in UTC. If the `timestamp`s are already localized, they'll be very confusing to people who understand ISO 8601 timezone declarations, because the timestamps will be displayed with a "+00:00" suffix. So they pretend to be UTC. (This was the case from 2017-2020 Databricks, I have not checked since - I currently don't use it anymore.)

So:

- In general, avoid using `timestamp` data type for other timezones than UTC.
- If you do want to have localized `timestamp`s with an explicit timezone, it's fair game to use strings with ISO 8601 timestamps inside. This is often a good idea as it makes perfectly clear to users in which timezone the time is, and it's straight forward to convert it using Spark's built-in functions. Also, sorting still works.

However, if you do use `timestamp` data type for a non-UTC time, here are some tips:

- Be explicit about it! Call the column `localTimestamp` instead of simply `timestamp` (or `localDateTime`, `localEventTime`, `eventDateTimeLocal`, and so on).
- Do not use tz-aware `datetime.datetime` objects when comparing non-UTC `timestamp`s in PySpark. Always compare with tz-naive local time `datetime`s.
- Be prepared for confusing displays in tools like Databricks. Hue may also be affected.
- Be prepared for ambiguous timestamps around daylight saving time switch (the same hour will be used twice once a year).

