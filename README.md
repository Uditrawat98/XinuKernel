# CSCI475-Proj4 Deadlock Detection and Recovery (xinu)
### Implementing time scheduling in Oracle VM VirtualBox ~5.1.14.

### This repository is being used as a collaborative workspace for project group memebers.

#### Project 4 ####
#### Authors: Jack Burns and Ian White ####

In this project we implemented a simple deadlock detection algorithm outside of xinu and then adjusted our xinu OS to work with that algorithm. The detection algorithm made use of a resource allocation graph to detect when a cycle occurred. In xinu we replaced the mutex_t locks with lockentry structs, which hold a mutex_t lock, a queue of waiting processes, and a state variable. We then implemented a RAG inside xinu to detect deadlocks every 50 times resesched was run. Deadlock recovery presented some problems, namely that actually killing the process holding the lock caused the program to stop entirely. So we killed the process later in the function. 

For our test case we implemented a more complex deadlock situation with two deadlocks. We expect a deadlock with lock 0 and pid 6, and another deadlock with lock 4, pid 2, lock 1, and pid 5. The processes are created in order of pid, and process 2 always takes lock 0 first. Processes 3, 4, 5, and 6 are created shortly after and take the next three locks (1, 2, 3, and 4). Because process 0 is requesting lock 3 while the rest of the processes are trying to access lock 0, deadlocks ensue. 
