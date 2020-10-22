#include <stdio.h>
#define MAX_SIZE 10

int front = -1, rear = -1;
int queue[MAX_SIZE];
void enqueue()
{
    if(rear == -1 && front == -1)
            front=0, rear = 0;
    else if(rear == MAX_SIZE-1){
        printf("Queue is full");
        return;
    }
    else rear += 1;
    printf("\nEnter value : ");
    scanf("%d",&queue[rear]);
    prtinf("\nValue added successfully\n");
}

void dequeue()
{
    if(rear == -1 && front == -1)
            printf("Queue is empty");
    else if(front==rear){
        printf("%d is removed",queue[front]);
        front=-1,rear=-1;
    }
    else{
        front+=1;
        printf("%d is removed",queue[front-1]);
    }
}

void display()
{
    if (rear == -1 && front == -1)
        printf("\nQueue is empty");
    else
    {
        printf("\nQueue elements are : ");
        for (int i = front; i <= rear; i++)
            printf("%d ", queue[i]);
        printf("\n");
    }
}

void perform_operation(int option)
{
    switch (option)
    {
    case 1:
        enqueue();
        break;
    case 2:
        dequeue();
        break;
    case 3:
        display();
        break;
    case 4:
        printf("\n----------Program ends----------\n");
        break;
    default:
        printf("\nSelect a valid option\n");
    }
}

void start_operation()
{
    int option;
    do
    {
        printf("\n1. Enqueue an Element on to Queue"
               "\n2. Dequeue an Element from Queue"
               "\n3. Display the elements of a Queue"
               "\n4. Exit\n");
        printf("\nSelect a option from above: ");
        scanf("%d", &option);
        perform_operation(option);
    } while (option != 4);
}

int main()
{
    printf("\n-----------Implementation of Queue using array-----------\n\n");
    start_operation();
    return 0;
}
