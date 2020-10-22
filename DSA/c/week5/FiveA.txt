#include <stdio.h>
#include <stdlib.h>
typedef struct Stack
{
    int data;
    struct Stack *next;
}Stack;
Stack *top=NULL;

void push(){
    Stack *node=(Stack*) malloc(sizeof(Stack));
    if(node==NULL){
        printf("\nMemory is full !!!\n");
        return;
    }
    printf("\nEnter value to be inserted : ");
    scanf("%d",&node->data);
    node->next=NULL;
    if(top==NULL){ 
        top=node;
    }else{
        node->next=top;
        top=node;
    }
    printf("\nValue pushed\n");
}

void peek(){
    if(top==NULL){
        printf("\nStack is empty\n");
        return;
    }
    printf("\n%d is present at the end of stack\n",top->data);
}

void pop(){
    if(top==NULL){
        printf("\nStack is empty\n");
    }else{
        int val=top->data;
        Stack* prev=top;
        top=top->next;
        free(prev);
        printf("\n%d is removed from the stack\n",val);
    }
}

void display(){
    printf("\nStack elements are: \n");
    int i=0;
    Stack* ptr=top;
    while(ptr!=NULL){
        printf("Element - %d : %d\n",i+1,ptr->data);
        ptr=ptr->next;
        i++;
    }
    printf("\n");
}

void finish(){
    Stack* prev=top;
    while (top!=NULL)
    {
        prev=top;
        top=top->next;
        free(prev);        
    }
    top=NULL;
}

void perform(int option){
    switch (option)
    {
    case 1:
        push();
        break;
    case 2:
        pop();
        break;
    case 3:
        peek();
        break;
    case 4:
        if(top==NULL) printf("\nThere are no elements to diaplay in stack\n");
        else display();
        break;
    case 5:
        finish();
        printf("\n~~~~~~~~~~~~~~~~~~~~~~~Program ends~~~~~~~~~~~~~~~~~~~~~~~\n");
        break;
    default:
        break;
    }

}
void start(){
    int option;
    do{
        printf("\n1. Push an element\n"
              "2. pop an element\n"
              "3. peek at top of stack\n"
              "4. Display stack\n"
              "5. Exit\n\n");
        printf("Select a option: ");
        scanf("%d",&option);
        perform(option);
    }while(option!=5);
}
int main(){
    printf("\n~~~~~~~~~~~~~~~~~~~~~~~~~~~~Implementation Of Stack with linked list~~~~~~~~~~~~~~~~~~~~~~~~~~~~\n");
    start();
    return 0;
}
