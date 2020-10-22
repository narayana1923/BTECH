#include <stdio.h>
#include <stdlib.h>

typedef struct queue
{
    int data;
    struct queue *next;
} Queue;
Queue *front = NULL;
Queue *rear = NULL;

void enqueue(){
    Queue *ptr=(Queue*) malloc(sizeof(Queue));
    if(ptr==NULL){
        printf("\nMemory is full\n");
        return;
    }
    printf("\nEnter value to be inserted: ");
    scanf("%d",&ptr->data);
    ptr->next=NULL;
    if(front==NULL){
        front=ptr;
        rear=ptr;
    }else{
        rear->next=ptr;
        rear=ptr;
    }
    printf("\nValue added\n");
}

void dequeue(){
    if(front==NULL){
        printf("\nQueue is empty\n");
    }else{
        Queue* prev=front;
        front=front->next;
        printf("\n%d is removed from the queue\n",prev->data);
        free(prev);
    }
}
void display(){
    Queue* ptr=front;
    printf("\nQueue elements are:\n");
    int i=0;
    while(ptr!=NULL){
        printf("\nElement - %d : %d",i+1,ptr->data);
        ptr=ptr->next;
        i++;
    }
    printf("\n");
}

void finish()
{
    Queue *prev = front;
    while (front!=NULL)
    {
        prev=front;
        front=front->next;
        free(prev);   
    }
    front=NULL;
    rear=NULL;
}

void perform(int option)
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
        if(front==NULL) printf("\nThere are no elements in queue\n");
        else display();
        break;
    case 4:
        finish();
        printf("\n~~~~~~~~~~~~~~~~~~~~~~~Program ends~~~~~~~~~~~~~~~~~~~~~~~\n");
        break;
    default:
        break;
    }
}
void start()
{
    int option;
    do
    {
        printf("\n1. Enqueue an element\n"
              "2. Dequeue an element\n"
              "3. Display stack\n"
              "4. Exit\n\n");
        printf("Select a option: ");
        scanf("%d",&option);
        perform(option);
    } while (option != 4);
}
int main()
{
    printf("\n~~~~~~~~~~~~~~~~~~~~~~~~~~~~Implementation Of Queue with linked list~~~~~~~~~~~~~~~~~~~~~~~~~~~~\n");
    start();
    return 0;
}
