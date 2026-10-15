## 1. Indexes



I would create a unique index on `employees.emp\_code` to prevent duplicate employees, and a unique compound index on `attendance\_logs (emp\_code, date)` to guarantee one attendance record per employee per day.



I would also create indexes to support attendance filtering and sorting, such as `(date, emp\_code)` and `(emp\_code, date)`. These help avoid collection scans for common attendance queries.



I considered a separate index on `department`, but would avoid adding it without evidence that it improves query performance, because every additional index increases storage and write costs.



## 2. Punch-in race



Two identical punch-in requests can arrive at the same time. Both may initially find that no attendance record exists. I rely on a unique compound index on `(emp\_code, date)` as the final safeguard.



The first insert succeeds and returns `201 Created`. The second insert violates the unique index and returns `409 Conflict`. I handle MongoDB duplicate-key errors explicitly so that a race does not create duplicate attendance records.



## 3. Ties



If two employees are tied on late minutes at the leaderboard cutoff, I include both employees. I use standard competition ranking, so tied employees receive the same rank and the next rank is skipped. The limit filters by rank rather than simply truncating the result to a fixed number of employees.



## 4. Headcount



I start the department summary from the employees collection and then use a `$lookup` to join attendance records for the requested month. This includes employees who have no attendance logs. I count only employees whose `joined\_on` date is on or before the end of the month, and exclude departments with zero eligible employees.



# 5. One thing I would change for 100x the data



I would review query execution plans and add or adjust indexes based on real workload measurements. I would also ensure that analytics use MongoDB aggregation pipelines instead of loading large collections into application memory, and introduce appropriate caching for frequently requested monthly summaries.

