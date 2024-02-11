Rarely, while optimizing Postgres, increasing work_mem can actually cause a query to run slower. 

For example, consider an operation whose complexity increases with the size of the dataset. If the work_mem is large, it can try to fit a very large dataset into memory, and make it slower to process. It would have been faster to process the dataset in smaller chunks, and then combine the results. It is also possible that a high work_mem causes the planner to process the entire dataset in a single thread instead of spawning parallel processes. This can also slow things down. In many cases, it is necessary to increase the value of shared_buffers, in addition to work_mem. It is also essential to thoroughly test when system settings are changed. 


https://dba.stackexchange.com/questions/27893/increasing-work-mem-and-shared-buffers-on-postgres-9-2-significantly-slows-down 

https://dba.stackexchange.com/questions/335535/cheaper-query-plan-takes-much-longer-to-execute/335583#335583 

On the flight tickets database:

explain (analyze, buffers) select boarding_no, ticket_no, count(seat_no) as a from boarding_passes group by 2, 1

explain (analyze, buffers) select flight_id, ticket_no, count(amount) as a from ticket_flights group by 2, 1 


