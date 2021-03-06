# CiggSmokersProblem

Contributors:

Faraz Murtaza	k16-4054
Okesh Kumar	k16-4026
Syed Hamza	k16-4059

# Introduction

The cigarette smokers’ problem is a concurrency problem in Computer Science, originally described in 1971 by Suhas Patil.
In this problem The Agent represents the Operating System and the smokers represent the processes/threads. In this problem, The Agent (Operating System) should allocate resources to smokers (Processes/Threads) and at the same time avoid Deadlock.

Assume a cigarette requires three ingredients to make and smoke: tobacco, paper, and matches. There are three smokers around a table, each of whom has an infinite supply of one of the three ingredients — one smoker has an infinite supply of tobacco, another has paper, and the third has matches.

There is also a non-smoking agent who enables the smokers to make their cigarettes by arbitrarily selecting two of the supplies to place on the table. The smoker who has the third supply should remove the two items from the table, using them (along with their own supply) to make a cigarette, which they smoke for a while. Once the smoker has finished his cigarette, the agent places two new random items on the table. This process continues forever.


# Getting Started

Installaton Procedure:

1. Open up Terminal By pressing ``` Ctrl + Alt + T ```
2. Type ``` sudo apt-get install git ``` to install git on your Linux machine.
3. After the installation is complete, type ``` git clone https://github.com/farazmurtaza/CiggSmokersProblem.git ```
4. Navigate to the target directory through terminal by ``` cd CiggSmokersProblem```
5. Compile the code by typing ``` gcc -o main main.c -lpthread ``` 
6. Execute the compiled program by typing ``` ./main ```

# Explanation

Three semaphores are used to represent the three smokers (``` semaphoreSmoker[3] ```); the agent (another semaphore: ```semaphoreAgent``` ) increases the appropriate semaphore to signal that an item has been placed on the table. Also, each smoker has an associated semaphore that they use to signal to the agent that they are done smoking (in this case: ``` smokerReady ```); the agent has a semaphore (``` agentReady ```) that waits on each smoker's semaphore to let it know that it can place the new items on the table. This cycle continues infinitely (for testing purposes, number of turns for each smoker is limited to 7, resulting 21 throws from the agent).

Additional Libraries Used: 
<semaphore.h>
<pthread.h>

# Glossary

1. Threads:

A thread of execution is the smallest sequence of programmed instructions that can be managed independently by a scheduler, which is typically a part of the operating system. The implementation of threads and processes differs between operating systems, but in most cases a thread is a component of a process. Multiple threads can exist within one process, executing concurrently and sharing resources such as memory, while different processes do not share these resources. In particular, the threads of a process share its executable code and the values of its variables at any given time. 

```
pthread_t: is the data-type for the threads being used that is included in the library pthread.

pthread_create(): is a function used to create threads. It requires four parameters: 
pthread_create(pthread_t *thread, const pthread_attr_t *attr, void *(*start_routine) (void *), void *arg);

pthread_join(): is also a function that shall suspend execution of the calling thread until the target thread terminates, unless the target thread has already terminated. This function requires two parameters:
pthread_join(pthread_t thread, void **value_ptr);
```
    
2. Semaphores:

A semaphore is a variable or abstract data type used to control access to a common resource by multiple processes in a concurrent system such as a multitasking operating system.

``` 
sem_t: is the data-type for semaphores.

sem_init(): is a function that is used to initialise the unnamed semaphore referred to by sem.
sem_init(sem_t *sem, int pshared, unsigned int value);
The sharing of the semaphore depends on the value of pshared, i.e. 0 for shared and 1 for unshared.

sem_wait(): it decrements (locks) the semaphore pointed to by sem. If the semaphore's value is greater than zero, then the decrement proceeds, and the function returns, immediately. If the semaphore currently has the value zero, then the call blocks until either it becomes possible to perform the decrement (i.e., the semaphore value rises above zero), or a signal handler interrupts the call.

sem_post(): The sem_post() function shall unlock the semaphore referenced by sem by performing a semaphore unlock operation on that semaphore. If the semaphore value resulting from this operation is positive, then no threads were blocked waiting for the semaphore to become unlocked; the semaphore value is simply incremented.
```
