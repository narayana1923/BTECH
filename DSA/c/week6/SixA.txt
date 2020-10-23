#include <stdio.h>
#include <string.h>
#define MAX_SIZE 200

char stack[MAX_SIZE];
char postfix[MAX_SIZE];
int top = -1;
char pop()
{
    return stack[top--];
}
void push(char j)
{
    top++;
    stack[top] = j;
}
char peek()
{
    return stack[top];
}
int is_operand(char ch)
{
    return (ch >= 'a' && ch <= 'z') || (ch >= 'A' && ch <= 'Z') || (ch>='0' && ch<='9');
}

int precedence(char operate)
{
    if (operate == '^')
        return 3;
    else if (operate == '*' || operate == '/')
        return 2;
    else if (operate == '+' || operate == '-')
        return 1;
    return 0;
}

char *infix_to_postfix(char infix[])
{
    int k = -1;
    for (int i = 0; i < strlen(infix); i++)
    {
        if (is_operand(infix[i]))
        {
            postfix[++k] = infix[i];
        }
        else if (infix[i] == '(')
        {
            push(infix[i]);
        }
        else if (infix[i] == ')')
        {
            while (top != -1 && peek() != '(')
            {
                postfix[++k] = pop();
            }
            if (top != -1)
                pop();
        }
        else
        {
            while (top != -1 && precedence(infix[i]) <= precedence(stack[top]))
                postfix[++k] = pop();
            push(infix[i]);
        }
    }
    while (top != -1 && peek() != '(')
        postfix[++k] = pop();
    postfix[++k] = '\0';
    return postfix;
}

int main()
{
    char infix[MAX_SIZE];
    printf("Enter infix Expression: ");
    scanf("%s", infix);
    printf("Postfix expression is %s\n", infix_to_postfix(infix));
    return 0;
}
