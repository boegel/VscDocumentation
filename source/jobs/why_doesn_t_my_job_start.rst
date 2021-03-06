Why doesn't my job start?
=========================

Jobs are submitted to a queue system, which is monitored by a scheduler
that determines when a job can be executed.

The latter depends on two factors:

#. the priority assigned to the job by the scheduler, and the priorities
   of the other jobs already in the queue, and
#. the availability of the resources required to run the job.

The priority of a job is calculated using a formula that takes into
account a number of factors:

#. the user's credentials (at the moment, all users are equal)
#. fair share: this takes into account the amount of walltime that the
   user has used over the last seven days, the more used, the lower the
   resulting priority
#. time queued: the longer a job spends in the queue, the larger its
   priority becomes, so that it will run eventually
#. requested resources: larger jobs get a higher priority

These factors are used to compute a weighted sum at each iteration of
the scheduler to determine a job's priority. Due to the time queued and
fair share, this is not static, but evolves over time while the job is
in the queue.

Different clusters use different policies as some clusters are optimised
for a particular type of job.

To get an idea when your job might start, you could try MOAB's
'showstart' command as described in the page on ":ref:`submitting jobs`".

Also, don't try to outsmart the scheduler by explicitly specifying nodes
that seem empty when you launch your job. The scheduler may be saving
these nodes for a job for which it needs multiple nodes, and the result
will be that you will have to wait even longer before your job starts as
the scheduler will not launch your job on another node which may be
available sooner.

Remember that the cluster is not intended as a replacement for a decent
desktop PC. Short, sequential jobs may spend quite some time in the
queue, but this type of calculation is atypical from a HPC perspective.
If you have large batches of (even relatively short) sequential jobs,
you can still pack them as longer sequential or even parallel jobs and
get to run them sooner. User support can help you with that.
