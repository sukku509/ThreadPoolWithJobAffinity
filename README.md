# ThreadPoolWithJobAffinity
ThreadPoolWithJobAffinity:
Implementation of a thread pool with job affinity

Each task submitted to the pool should be identified with a distinct job id. Based on the id, either a new worker thread is spawned or an existing thread is used and the job is queued. The thread pool guarantees that jobs having the same id are executed by the same worker thread.

Assumptions:

•	Implemented fixed thread pool as a part of this implementation, (Number of unique jobs = Thread pool size.)

•	Main program of this application is: MainThreadPoolDemo

•	for each JOBID a queue is taken in a HASHMAP of <JOBID, QUEUE> (jobQueueMap)

•	In the current approach I have used Queue data structure and taken care of explicit synchronization, improvement is to use BlockingQueue/SynchronousQueue would give better performance.

•	If JOBID "x" are present in HASHMAP then thread enters its critical section and get a handle of the QUEUE removes the entry from QUEUE and execute jobs. Suppose Thread-X was executing jobs with JOBID "x", now if another Thread-Y comes with JOBID "y", then its takes the control of its dedicated queue associated with it in shared data structure.

•	With JOBID "x" will be executed only with Thread-X not with any other thread.

•	Thread pool size in my implementation is the size of jobQueueMap. (We can easily change this to size of thread pool)

•	Distribution of jobs taken care by random number generator across the worker threads.

Usage Examples:

Usage is covered in the unit tests.

•	ThreadPoolWithJobAffinityTest- Unit test for the thread pool.
