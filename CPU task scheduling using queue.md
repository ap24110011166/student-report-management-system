\#include <stdio.h>

\#include <stdlib.h>

\#include <string.h>



\#define MAX 50



// Structure to store each task

typedef struct {

&nbsp;   int id;

&nbsp;   char name\[30];

&nbsp;   int burstTime;

} Task;



// Queue variables

Task queue\[MAX];

int front = -1, rear = -1;



// Function prototypes

void enqueue(Task t);

Task dequeue();

int isEmpty();

void displayQueue();



int main() {

&nbsp;   int choice;

&nbsp;   int taskID = 1;



&nbsp;   while (1) {

&nbsp;       printf("\\n================ CPU TASK SCHEDULING (FIFO) ================\\n");

&nbsp;       printf("1. Add Task\\n");

&nbsp;       printf("2. Execute Next Task\\n");

&nbsp;       printf("3. Display Waiting Tasks\\n");

&nbsp;       printf("4. Exit\\n");

&nbsp;       printf("Choose an option: ");

&nbsp;       scanf("%d", \&choice);



&nbsp;       if (choice == 1) {

&nbsp;           Task t;

&nbsp;           t.id = taskID++;



&nbsp;           printf("Enter task name: ");

&nbsp;           scanf("%s", t.name);



&nbsp;           printf("Enter burst time (ms): ");

&nbsp;           scanf("%d", \&t.burstTime);



&nbsp;           enqueue(t);



&nbsp;           printf("\\nTask added successfully.\\n");

&nbsp;       }



&nbsp;       else if (choice == 2) {

&nbsp;           if (isEmpty()) {

&nbsp;               printf("\\nNo tasks to execute. Queue is empty.\\n");

&nbsp;           } else {

&nbsp;               Task exec = dequeue();

&nbsp;               printf("\\nExecuting Task...\\n");

&nbsp;               printf("Task ID: %d\\n", exec.id);

&nbsp;               printf("Task Name: %s\\n", exec.name);

&nbsp;               printf("Burst Time: %d ms\\n", exec.burstTime);

&nbsp;               printf("Task execution completed.\\n");

&nbsp;           }

&nbsp;       }



&nbsp;       else if (choice == 3) {

&nbsp;           displayQueue();

&nbsp;       }



&nbsp;       else if (choice == 4) {

&nbsp;           printf("\\nExiting the scheduler.\\n");

&nbsp;           break;

&nbsp;       }



&nbsp;       else {

&nbsp;           printf("\\nInvalid choice. Try again.\\n");

&nbsp;       }

&nbsp;   }



&nbsp;   return 0;

}



// ------------------------------------------------------

// ENQUEUE FUNCTION

// ------------------------------------------------------

void enqueue(Task t) {

&nbsp;   if (rear == MAX - 1) {

&nbsp;       printf("\\nQueue is full. Cannot add more tasks.\\n");

&nbsp;       return;

&nbsp;   }



&nbsp;   if (front == -1)

&nbsp;       front = 0;



&nbsp;   rear++;

&nbsp;   queue\[rear] = t;

}



// ------------------------------------------------------

// DEQUEUE FUNCTION

// ------------------------------------------------------

Task dequeue() {

&nbsp;   Task t;



&nbsp;   if (isEmpty()) {

&nbsp;       printf("\\nQueue is empty.\\n");

&nbsp;       t.id = -1;

&nbsp;       return t;

&nbsp;   }



&nbsp;   t = queue\[front];

&nbsp;   front++;



&nbsp;   if (front > rear) {

&nbsp;       front = rear = -1;

&nbsp;   }



&nbsp;   return t;

}



// ------------------------------------------------------

// CHECK EMPTY

// ------------------------------------------------------

int isEmpty() {

&nbsp;   return (front == -1);

}



// ------------------------------------------------------

// DISPLAY QUEUE

// ------------------------------------------------------

void displayQueue() {

&nbsp;   if (isEmpty()) {

&nbsp;       printf("\\nNo tasks in the queue.\\n");

&nbsp;       return;

&nbsp;   }



&nbsp;   printf("\\nTasks waiting in queue:\\n");

&nbsp;   printf("------------------------------------------\\n");

&nbsp;   for (int i = front; i <= rear; i++) {

&nbsp;       printf("Task ID: %d | Name: %s | Burst: %d ms\\n",

&nbsp;              queue\[i].id,

&nbsp;              queue\[i].name,

&nbsp;              queue\[i].burstTime);

&nbsp;   }

&nbsp;   printf("------------------------------------------\\n");

}



