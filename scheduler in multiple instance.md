# Scheduler in multiple instance.

### Problem.

Running multiple instance of microservice/app which implemented `scheduler` will lead multiple problem. 

  Example: Sending daily notification to customers. If there are 10 running instance, then each customer will recieve 10 notification with same message.
  
  
### Solution

Store the scheduler information in the database and lock the scheduler 

(First instance which it starts the scheduler checks the database, 

1. If there is no lock it inserts the scheduler lock information and starts the scheduler.
2. If there is any lock information in the database then ignore the scheduler task)

Spring boot libraries [shedlock-spring](https://github.com/lukas-krecan/ShedLock)

Eg: `@SchedulerLock(name = "notify", lockAtMostFor = "3m", lockAtLeastFor = "2m")`
