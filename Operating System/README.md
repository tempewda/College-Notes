Reference: https://youtube.com/playlist?list=PLxCzCOWd7aiGz9donHRrE9I3Mwn6XdP8p

# Operating System

- what?
    - system software
    - works as an interface between User and Hardware
- why?
    1. Primary Goal
        1. Convenience: Easy to use
        2. Throughput: number of tasks executed per unit time
    2. Major Goal
        1. Resource Management
        2. Process Management: CPU Scheduling
        3. Storage Management: Hard Disk
        4. Memory Management: RAM
        5. Security
- types
    1. Batch
        1. Grouping similar processes into batches and then executing them non-preemptively
    
    2. Multiprogrammed
        1. Loads multiple programs in RAM n then gives them to CPU for execution non preemptively
        2. Main goal: reduce CPU idleness
    
    3. Multitasking/Time Sharing OS
        1.  CPU can execute a single process only for a limited unit time, aftr which it switches to next process in queue. Preemptive execution
        2. Main goal: responsiveness, no process has to wait for a long time in queue
    
    4. Real Time OS
        1. Immediate output frm the computer, where delays aren't an option
        2. Can b categorised into Hard and Soft, depending on the delay that can be tolerated
    
    5. Distributed
    6. Clustered
    7. Embedded

# Process vs Threads

| Process | Threads |
| ---- | ---- |
| Occurs at system level, so system calls are involved | Occurs at user level, so no system calls involved |
| OS treats different tasks differently | OS treats all threads as a single task |
| Blocking one process does not affect the other processes | Blocking a thread blocks the entire process/ all the other threads |
| Independent from one another | Interdependent on one other |
| Each has different copies of data, code | Threads share same copy of data and code; but they have different copies of stack and registers |
| Context switching is slower <br>process switching occurs aftr a particular time quantum so all the values of the process has to be stored by PCB b4 switching, which makes it time consuming | Context switching is faster <br>sharing of code/data occurs so no switching n saving of values is needed switching of registers may occur but it isn’t as time consuming |


![creation of child process using fork()](Operating%20System%2053855acbcafc4abdbbcee389d23000f5/Untitled.png)

creation of child process using fork()

![Threads share code/data but have different copies of stacks/registers](Operating%20System%2053855acbcafc4abdbbcee389d23000f5/Untitled%201.png)

Threads share code/data but have different copies of stacks/registers

# Process States

![[Pasted image 20240128102442.png]]

- Long Term Scheduler
    Moves a process frm New to Ready state

- Short Term Scheduler
    Moves a process frm Ready to Running state

- Medium Term Scheduler
    If the wait/block queue is full, it moves frm wait/block to suspend wait queue
    If the ready queue is full, it moves frm ready to suspend ready queue

- Backing Store
    If a process frm suspend wait queue, wants to get to running state, but the wait/block queue is already filled, then it can b moved frm suspend wait to suspend ready, thru backing store method


# Process Scheduling

- why?
    - single-processor system supports only 1 process at a time so others wait till CPU is free
    - if process being executed waits for completion of I/O requests, in that case CPU sits idle the whole time, leading to wastage of time
    - multiprogramming maximizes CPU utilization - some process running at all times
    - it tries to use this idle time productively - when one process has to wait, OS takes the CPU away from that process and gives the CPU to another process
    - choosing which process to run requires some scheduling

- what?
	- moves processes from Ready to Running State
    - deals with the problem of deciding which of the processes in the ready queue is to be allocated to the CPU (running state)

- terminology
    - Arrival time
        point of time at which a process enters the ready start/queue
    
    - Burst time
        time required by a process for execution 
    
    - Completion time
        point of time at which a process completes its execution
    
    - Turn around Time
        Completion time - Arrival time
    
    - Waiting time
        Turn around time - Burst time
    
    - Response time
        point of time at which the process got CPU for first time - Arrival time
    
- types
    - FCFS
        - first - come, first - served
        - process that requests the CPU first is allocated the CPU first
        - avg waiting time is often quite long
        - Convoy effect
            all the other processes wait for one big process to get off the cpu. this results in lower cpu and device utilization than might be possible if the shorter processes were allowed to go first
            
    - SJF
        - Shortest job first
        - associates with each process, the length of the process' next cpu burst
        - when cpu is available, it is allocated to the process with the shortest next cpu burst
        - if bursts of 2 process r same, fcfs is followed on them
        - shortest-remaining-time-first
            
            if a new process arrives at the ready queue, with a next cpu burst time shorter than what is left of the currently executing process, the current process is preempted.
            
    - Priority Scheduling
        - a priority is associated with each process, cpu is allocated to the process with highest priority
        - larger the cpu burst, lower the priority
        - starvation / indefinite blocking
            - this scheduling can leave some low priority processes waiting indefinitely
            - a steady stream of high priority processes can prevent the low priority process from ever getting the cpu
        - aging
            
            involves gradually increasing the priority of the processes that wait in the system for a long time
            
    - Round Robin Scheduling
        - similar to fcfs but preemption is added to enble the system to switch between processes
        - a small unit of time, called time quantum or time slice, is defined
        - ready queue is treated as a circular queue
        - cpu scheduler goes around the ready queue, allocating the cpu to each process for a time interval of up to 1 time quantum

# Deadlock

- what?
    - In a multiprogramming environment, several threads may compete for a finite number of resources.
    - A thread requests resources; if the resources are not available at that time, the thread enters a waiting state.
    - Sometimes, a waiting process can never again change state, because the resources it has requested are held by other waiting processes. This situation is called a deadlock
    
    > a situation in which every process in a set of processes is waiting for an event that can be caused only by another process in the set
    > 
- how?
    
    necessary conditions for deadlock to take place:
    
    1. mutual exclusion : at least one resource must be held in a non-sharable mode; that is, only one process at a time can use the resource. if another process requests that resource, the requesting process must be delayed until the resource has been released
    2. hold and wait : a process must be holding at least one resource and waiting to acquire additional resources that are currently being held by other processes
    3. no preemption : resources can't be preempted; that is, a resource can be released only voluntarily by the process holding it, after that process has completed its task
    4. circular wait : A set {T0, T1, ..., Tn} of waiting processes must exist such that T0 is waiting for a resource held by T1, T1 is waiting for a resource held by T2, ..., Tn−1 is waiting for a resource held by Tn, and Tn is waiting for a resource held by T0.

# System Call

### File Related

- open()
- Read()
- Write ()
- Close()
- Create file

### Device Related

To access the hardwares

- Read
- Write
- Reposition - repositioning the values or accessing its attributes
- IOCtrl - control the input output devices

### Information Related

Get metadata, or info related to a particular process

- get [Pid()](https://www.geeksforgeeks.org/getppid-getpid-linux/) - process id
- Attributes
- get System date and time

### Process Control

- Load
- Execute
- Abort
- [Fork](https://www.notion.so/Fork-System-Call-e2aa2db21af240a1b4b43b0cdaa9a7ed?pvs=21)
- Wait
- Signal
- Allocate, etc.

### Communication

Inter-process communication i.e. communication between 2 processes

- [Pipe ()](https://www.geeksforgeeks.org/pipe-system-call/)
- Shmget() - get shared memory
- create/delete connections
