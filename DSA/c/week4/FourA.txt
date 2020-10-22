#include <stdio.h>
#define MAX_SIZE 10

int top = -1;
int stack[MAX_SIZE];
void push()
{
    if (top + 1 == MAX_SIZE)
    {
        printf( "\nStack is full, Cannot insert elements!!\n");
    }
    else
    {
        printf( "\nEnter value to be inserted: ");
        scanf("%d",&stack[++top]);
        printf( "\nElement successfully pushed into the stack\n");
    }
}

int pop(int *s,int *t)
{
    int popped_value = s[*t];
    (*t)--;
    return popped_value;
}

void palindrome()
{
    if (top == -1)
    {
        printf( "\nStack is empty, palindrome operation not possible\n");
    }
    else
    {
        int temp_stack[MAX_SIZE];
        int top2 = top;
        for (int i = 0; i <= top; i++)
            temp_stack[i] = stack[i];
        int x = 1;
        for (int i = 0; i <= (top / 2); i++)
        {
            if (temp_stack[i] != pop(temp_stack,&top2))
            {
                x = 0;
                break;
            }
        }
        printf("\nStack is %s\n",(x ? "palindrome" : "not palindrome"));
    }
}

void display()
{
    if (top == -1)
    {
        printf( "\nThere are no elements to display in stack\n");
    }
    else
    {
        printf( "\nStack elements are:\n\n");
        for (int i = top; i >=0; i--)
        {
            printf( "Element - %d : %d\n",i + 1,stack[i]);
        }
        printf("\n");
    }
}

void perform_operation(int option)
{
    switch (option)
    {
    case 1:
        push();
        break;
    case 2:
        if (top == -1)
        {
            printf( "\nStack is empty, pop is not possible!!!\n");
        }
        else
        {
            printf( "\n%d,popped out of the stack\n",pop(stack,&top));
        }
        break;
    case 3:
        palindrome();
        break;
    case 4:
        display();
        break;
    case 5:
        printf( "\n----------Program ends----------\n");
        break;
    default:
        printf( "\nSelect a valid option\n");
    }
}

void start_operation()
{
    int option;
    do
    {
        printf( "\n1. Push an Element on to Stack"
              "\n2. Pop an Element from Stack"
              "\n3. Check Palindrome"
              "\n4. Display the elements of a Stack"
              "\n5. Exit\n");
        printf( "\nSelect a option from above: ");
        scanf("%d",&option);
        perform_operation(option);
    } while (option != 5);
}

int main()
{
    printf( "\n-----------Implementation of Stack using array-----------\n\n");
    start_operation();
    return 0;
}
