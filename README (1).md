# cca-lab1

## Task 1

To clone the repository and perform basic Git operations:

```
D:
cd <directory-name>
git clone https://github.com/ashworks-png/cca-lab1.git
git status
git add .  # OR git add sample.txt
git commit -m "initial commit"
git push origin main
git fetch origin
git pull origin main
git branch a1
git branch
git branch -M a1
git checkout -b a2
git checkout a1  # to switch branches
git reset --soft a1
git branch -d a1  # to delete a1 branch
git rm <file-name>  # to delete a file from repo
```
## Task 2

Stack:

```
// C Program to demonstrate how to Implement a Stack
#include <stdio.h>
#include <stdbool.h>

// Define the maximim capacity of the stack
#define MAX_SIZE 100

// Define a structure for the stack
typedef struct {
    // Array to store stack elements
    int arr[MAX_SIZE];  
    // Index of the top element in the stack
    int top;        
} Stack;

// Function to initialize the stack
void initialize(Stack *stack) {
    // Set top index to -1 to indicate an empty stack
    stack->top = -1;  
}

// Function to check if the stack is empty
bool isEmpty(Stack *stack) {
    // If top is -1, the stack is empty
    return stack->top == -1;  
}

// Function to check if the stack is full
bool isFull(Stack *stack) {
    // If top is MAX_SIZE - 1, the stack is full
    return stack->top == MAX_SIZE - 1;  
}

// Function to push an element onto the stack
void push(Stack *stack, int value) {
    // Check for stack overflow
    if (isFull(stack)) {
        printf("Stack Overflow\n");
        return;
    }
    // Increment top and add the value to the top of the stack
    stack->arr[++stack->top] = value;
    printf("Pushed %d onto the stack\n", value);
}

// Function to pop an element from the stack
int pop(Stack *stack) {
    // Check for stack underflow
    if (isEmpty(stack)) {
        printf("Stack Underflow\n");
        return -1;
    }
    // Return the top element 
    int popped = stack->arr[stack->top];
    // decrement top pointer
    stack->top--;
    printf("Popped %d from the stack\n", popped);
    // return the popped element
    return popped;
}

// Function to peek the top element of the stack
int peek(Stack *stack) {
    // Check if the stack is empty
    if (isEmpty(stack)) {
        printf("Stack is empty\n");
        return -1;
    }
    // Return the top element without removing it
    return stack->arr[stack->top];
}

int main() {
    Stack stack;
    // Initialize the stack
    initialize(&stack);  

    // Push elements onto the stack and print the stack after each push
    push(&stack, 3);
    printf("Top element: %d\n", peek(&stack));

    push(&stack, 5);
    printf("Top element: %d\n", peek(&stack));

    push(&stack, 2);
    printf("Top element: %d\n", peek(&stack));

    push(&stack, 8);
    printf("Top element: %d\n", peek(&stack));

    // Pop elements from the stack and print the stack after each pop
    while (!isEmpty(&stack)) {
        printf("Top element: %d\n", peek(&stack));
        printf("Popped element: %d\n", pop(&stack));
    }

    return 0;
}
```

Queue:

```
// Queue implementation in C

#include <stdio.h>
#define SIZE 5

void enQueue(int);
void deQueue();
void display();

int items[SIZE], front = -1, rear = -1;

int main() {
  //deQueue is not possible on empty queue
  deQueue();

  //enQueue 5 elements
  enQueue(1);
  enQueue(2);
  enQueue(3);
  enQueue(4);
  enQueue(5);

  // 6th element can't be added to because the queue is full
  enQueue(6);

  display();

  //deQueue removes element entered first i.e. 1
  deQueue();

  //Now we have just 4 elements
  display();

  return 0;
}

void enQueue(int value) {
  if (rear == SIZE - 1)
    printf("\nQueue is Full!!");
  else {
    if (front == -1)
      front = 0;
    rear++;
    items[rear] = value;
    printf("\nInserted -> %d", value);
  }
}

void deQueue() {
  if (front == -1)
    printf("\nQueue is Empty!!");
  else {
    printf("\nDeleted : %d", items[front]);
    front++;
    if (front > rear)
      front = rear = -1;
  }
}

// Function to print the queue
void display() {
  if (rear == -1)
    printf("\nQueue is Empty!!!");
  else {
    int i;
    printf("\nQueue elements are:\n");
    for (i = front; i <= rear; i++)
      printf("%d  ", items[i]);
  }
  printf("\n");
}
```

Linked List:

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Define the structure for an employee
typedef struct Employee {
    char name[100];
    char email[100];
    char phoneNo[15];
    char designation[50];
    double salary;
    struct Employee* next;
} Employee;

// Function to create a new employee node
Employee* createEmployee(char name[], char email[], char phoneNo[], char designation[], double salary) {
    Employee* newEmployee = (Employee*)malloc(sizeof(Employee));
    strcpy(newEmployee->name, name);
    strcpy(newEmployee->email, email);
    strcpy(newEmployee->phoneNo, phoneNo);
    strcpy(newEmployee->designation, designation);
    newEmployee->salary = salary;
    newEmployee->next = NULL;
    return newEmployee;
}

// Function to add an employee to the linked list
void addEmployee(Employee** head, char name[], char email[], char phoneNo[], char designation[], double salary) {
    Employee* newEmployee = createEmployee(name, email, phoneNo, designation, salary);
    newEmployee->next = *head;
    *head = newEmployee;
    printf("Employee added successfully.\n");
}

// Function to delete an employee by name
void deleteEmployee(Employee** head, char name[]) {
    Employee* temp = *head;
    Employee* prev = NULL;

    // If the head node itself holds the employee to be deleted
    if (temp != NULL && strcmp(temp->name, name) == 0) {
        *head = temp->next; // Changed head
        free(temp); // Free old head
        printf("Employee deleted successfully.\n");
        return;
    }

    // Search for the employee to be deleted, keep track of the previous node
    while (temp != NULL && strcmp(temp->name, name) != 0) {
        prev = temp;
        temp = temp->next;
    }

    // If employee was not present in linked list
    if (temp == NULL) {
        printf("Employee not found.\n");
        return;
    }

    // Unlink the node from linked list
    prev->next = temp->next;
    free(temp); // Free memory
    printf("Employee deleted successfully.\n");
}

// Function to print the employee list
void printEmployees(Employee* head) {
    Employee* temp = head;
    if (temp == NULL) {
        printf("No employees to display.\n");
        return;
    }
    while (temp != NULL) {
        printf("Name: %s\n", temp->name);
        printf("Email: %s\n", temp->email);
        printf("Phone No: %s\n", temp->phoneNo);
        printf("Designation: %s\n", temp->designation);
        printf("Salary: %.2f\n", temp->salary);
        printf("-------------------------\n");
        temp = temp->next;
    }
}

// Main function to demonstrate the functionality
int main() {
    Employee* head = NULL;
    int choice;
    char name[100], email[100], phoneNo[15], designation[50];
    double salary;

    do {
        printf("\nEmployee Management System\n");
        printf("1. Add Employee\n");
        printf("2. Delete Employee\n");
        printf("3. View Employees\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter name: ");
                scanf("%s", name);
                printf("Enter email: ");
                scanf("%s", email);
                printf("Enter phone number: ");
                scanf("%s", phoneNo);
                printf("Enter designation: ");
                scanf("%s", designation);
                printf("Enter salary: ");
                scanf("%lf", &salary);
                addEmployee(&head, name, email, phoneNo, designation, salary);
                break;
            case 2:
                printf("Enter name of the employee to delete: ");
                scanf("%s", name);
                deleteEmployee(&head, name);
                break;
            case 3:
                printEmployees(head);
                break;
            case 4:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid choice! Please try again.\n");
                break;
        }
    } while (choice != 4);

    return 0;
}
```

Matrix Multiplication:

```
#include <stdio.h>

void multiplyMatrices(int firstMatrix[][10], int secondMatrix[][10], int resultMatrix[][10], int rowFirst, int columnFirst, int rowSecond, int columnSecond) {
    // Initializing all elements of resultMatrix to 0
    for (int i = 0; i < rowFirst; i++) {
        for (int j = 0; j < columnSecond; j++) {
            resultMatrix[i][j] = 0;
        }
    }

    // Multiplying firstMatrix and secondMatrix and storing in resultMatrix
    for (int i = 0; i < rowFirst; i++) {
        for (int j = 0; j < columnSecond; j++) {
            for (int k = 0; k < columnFirst; k++) {
                resultMatrix[i][j] += firstMatrix[i][k] * secondMatrix[k][j];
            }
        }
    }
}

void printMatrix(int matrix[][10], int row, int column) {
    for (int i = 0; i < row; i++) {
        for (int j = 0; j < column; j++) {
            printf("%d ", matrix[i][j]);
        }
        printf("\n");
    }
}

int main() {
    int firstMatrix[10][10], secondMatrix[10][10], resultMatrix[10][10];
    int rowFirst, columnFirst, rowSecond, columnSecond;

    // Input dimensions of first matrix
    printf("Enter rows and columns for the first matrix: ");
    scanf("%d %d", &rowFirst, &columnFirst);

    // Input dimensions of second matrix
    printf("Enter rows and columns for the second matrix: ");
    scanf("%d %d", &rowSecond, &columnSecond);

    // Check if multiplication is possible
    if (columnFirst != rowSecond) {
        printf("Error! Column of the first matrix must be equal to row of the second matrix.\n");
        return -1;
    }

    // Input elements of first matrix
    printf("Enter elements of the first matrix:\n");
    for (int i = 0; i < rowFirst; i++) {
        for (int j = 0; j < columnFirst; j++) {
            scanf("%d", &firstMatrix[i][j]);
        }
    }

    // Input elements of second matrix
    printf("Enter elements of the second matrix:\n");
    for (int i = 0; i < rowSecond; i++) {
        for (int j = 0; j < columnSecond; j++) {
            scanf("%d", &secondMatrix[i][j]);
        }
    }

    // Multiply matrices
    multiplyMatrices(firstMatrix, secondMatrix, resultMatrix, rowFirst, columnFirst, rowSecond, columnSecond);

    // Display the resulting matrix
    printf("Product of the matrices:\n");
    printMatrix(resultMatrix, rowFirst, columnSecond);

    return 0;
}
```

## Task 3

Steps to enable API and run a Python server:

```
Go to console.cloud.google.com
Enable API -> search for 'App Engine Admin API'
Open terminal (top-right) and execute the following commands:

git clone https://github.com/ashworks-png/cca-lab1.git
cd cca-lab1
python3 -m http.server 8000
```

## Task 4

Example Java code (fcfc-code.java) for process scheduling:

```
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter number of processes: ");
        int n = scanner.nextInt();

        int[] arrivalTime = new int[n];
        int[] burstTime = new int[n];
        int[] completionTime = new int[n];
        int[] turnaroundTime = new int[n];
        int[] waitingTime = new int[n];

        // Input arrival times and burst times
        for (int i = 0; i < n; i++) {
            System.out.print("Enter arrival time for process " + (i + 1) + ": ");
            arrivalTime[i] = scanner.nextInt();
            System.out.print("Enter burst time for process " + (i + 1) + ": ");
            burstTime[i] = scanner.nextInt();
        }

        // Calculate completion time for each process
        completionTime[0] = arrivalTime[0] + burstTime[0];
        for (int i = 1; i < n; i++) {
            completionTime[i] = completionTime[i - 1] + burstTime[i];
        }

        // Calculate turnaround time and waiting time for each process
        for (int i = 0; i < n; i++) {
            turnaroundTime[i] = completionTime[i] - arrivalTime[i];
            waitingTime[i] = turnaroundTime[i] - burstTime[i];
        }

        // Calculate average turnaround time and average waiting time
        double avgTurnaroundTime = 0;
        double avgWaitingTime = 0;
        for (int i = 0; i < n; i++) {
            avgTurnaroundTime += turnaroundTime[i];
            avgWaitingTime += waitingTime[i];
        }
        avgTurnaroundTime /= n;
        avgWaitingTime /= n;

        // Display results
        System.out.println("\nProcess\t Arrival Time\t Burst Time\t Completion Time\t Turnaround Time\t Waiting Time");
        for (int i = 0; i < n; i++) {
            System.out.println((i + 1) + "\t\t " + arrivalTime[i] + "\t\t " + burstTime[i] + "\t\t " + completionTime[i]
                    + "\t\t " + turnaroundTime[i] + "\t\t " + waitingTime[i]);
        }
        System.out.println("\nAverage Turnaround Time: " + avgTurnaroundTime);
        System.out.println("Average Waiting Time: " + avgWaitingTime);

        scanner.close();
    }
}
```
