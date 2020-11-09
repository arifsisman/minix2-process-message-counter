# Process Message Counter on Minix 2

## 1.DESCRIPTION

In computer science, message passing sends a message to a process (which may be an actor or object) and relies on the process and the supporting infrastructure to select and invoke the actual code to run. Message passing differs from conventional programming where a process, subroutine, or function is directly invoked by name.
Message passing is key to some models of concurrency and object-oriented programming.

Minix uses a message-passing paradigm to send and receive information among the processes for IPC purposes.

**Problem:** We want to count the messages between process i and j. After counting the messages, we want to print them on screen with user-friendly format when the F4 key is hit.

## 2.SOLUTION

Minix v2.0.4 under the usr/src/kernel changes were made.

First I have added a struct in glo.h to store the pieces of information properly. I've tried to store them in a linked list, but I had trouble in memory allocation operation
while adding items into the list.

Then I have created an array of structs which size of 60 in glo.h.

<p align="center">
    <img src="screenshots/glo.h_variables.png" width="600" />
    glo.h Variables
</p>

I have added a global integer for track the processes globally.

In usr/src/kernel/proc.c I have created a function named addList(int src,int dst) to store the process informations and counters.Then I have modified mini\*send function.

<p align="center">
    <img src="screenshots/proc.c_addList.png" width="600" />
    proc.c addList function
</p>

In mini_send function first I store caller_ptr pointers p_nr field as an integer named psource then I have called the addList function before the return statement with

psource and dest parameters which dest already exists in mini\*send function.

<p align="center">
    <img src="screenshots/proc.c_addList_call.png" width="600" />
    proc.c addList call in mini_send  
</p>

Finally, I have modified usr/src/kernel/keyboard.c. I have added a function to print
the array and call it when the F4 key is hit.
<p align="center">
<img src="screenshots/keyboard.c_printList.png" width="600" />
keyboard.c printList function

<img src="screenshots/keyboard.c_printList_call.png" width="600" />
keyboard.c printList on F4
</p>

After all these steps I have recompiled the OS in usr/src/tools with “make hdboot”

<p align="center">
    <img src="screenshots/process_message_counter_table.png" width="600" />
    Process Message Counter Table
</p>


## 3.REFERENCES

- https://en.wikipedia.org/wiki/Message_passing
