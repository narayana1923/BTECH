#include <stdio.h>
#include <math.h>
#include <string.h>
#include <stdlib.h>
#define MAX_SIZE 100
double stack[MAX_SIZE];
int top = -1;
double pop()
{
    if (top != -1)
        return stack[top--];
    else
        return '#';
}
void push(double j)
{
    if(top==MAX_SIZE-1){
        printf("Stack is full");
        exit(0);
    }
    stack[++top] = j;
}
char peek()
{
    return stack[top];
}

int is_operator(char ch)
{
    return ch == '+' || ch == '*' || ch == '-' || ch == '^' || ch == '/';
}

int is_digit(char ch){
    return ch>='0' && ch<='9';
}

void postfix_evaluvation(char postfix[])
{
    int postfix_value = 0;
    for (int i=0;i<strlen(postfix);i++)
    {
        if (!is_operator(postfix[i]) && !is_digit(postfix[i]))
        {
            printf("Invalid Expression!!!");
            return;
        }
        else if (is_digit(postfix[i]))
        {
            push(postfix[i] - '0');
        }
        else if (is_operator(postfix[i]))
        {
            double operand2 = pop();
            double operand1 = pop();
            switch (postfix[i])
            {
            case '+':
                push(operand1 + operand2);
                break;
            case '*':
                push(operand1 * operand2);
                break;
            case '/':
                push(operand1 / operand2);
                break;
            case '-':
                push(operand1 - operand2);
                break;
            case '^':
                push(pow(operand1, operand2));
                break;
            }
        }
    }
    printf("postfix value is %.2f\n",(double)peek());
}

int main()
{
    char postfix[MAX_SIZE];
    printf("Enter postfix expression to evaluate: ");
    scanf("%s",postfix);
    postfix_evaluvation(postfix);
    return 0;
}
