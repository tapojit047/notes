# Jobs
## *Chapter - 12*
- While long-running processes make up the large majority of
workloads that run on a Kubernetes cluster, there is often a need to run short-lived,
one-off tasks. The Job object is made for handling these types of tasks.
- A Job creates Pods that run until successful termination.
- Jobs are useful for things you only want to do once, such as database migrations or batch jobs.
- The Job object is responsible for creating and managing Pods defined in a template in
the job specification. These Pods generally run until successful completion.

Links: https://github.com/ishtiaqhimel/notes/blob/master/kubernetes/jobs.md
https://www.youtube.com/watch?v=j1EnBbxSz64&list=PLMPZQTftRCS8Pp4wiiUruly5ODScvAwcQ&index=36