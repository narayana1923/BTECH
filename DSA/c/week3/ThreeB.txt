#include <stdio.h>
#include <stdlib.h>
typedef struct node
{
    int emp_id, emp_mobileno;
    double emp_sal;
    char emp_dept[20];
    struct node *next;
    struct node *prev;
} Node;
int count = 0;
Node *head = NULL;
Node *last = NULL;
Node *searchNode(int id)
{
    Node *temp = NULL;
    Node *ptr = head;
    while (ptr != NULL)
    {
        if (ptr->emp_id == id)
        {
            temp = ptr;
            break;
        }
        ptr = ptr->next;
    }
    return temp;
}

Node *create(int id)
{
    Node *temp = (Node *)malloc(sizeof(Node));
    temp->emp_id = id;
    printf("Enter employee mobile no : ");
    scanf("%d", &temp->emp_mobileno);
    printf("Enter employee salary: ");
    scanf("%lf", &temp->emp_sal);
    fflush(stdin);
    printf("Enter employee dept : ");
    scanf("%[^\n]", temp->emp_dept);
    temp->next = NULL;
    temp->prev = NULL;
    printf("\n");
    count++;
    return temp;
}
void insertAtEnd()
{
    int id;
    printf("Enter employee id : ");
    scanf("%d", &id);
    fflush(stdin);
    if (searchNode(id) != NULL)
    {
        printf("\nEmployee already exists in DLL\n");
    }
    else
    {
        Node *temp = create(id);
        if (head->next == NULL)
        {
            last = temp;
            head->next = last;
            last->prev = head;
            return;
        }
        last->next = temp;
        temp = last;
        last = last->next;
        last->prev = temp;
    }
}
void add()
{
    int n, i = 1;
    printf("\nEnter number of employees you want to add: ");
    scanf("%d", &n);
    Node *temp;
    int id;
    if (head == NULL)
    {
        printf("---------------Enter Employee - %d details---------------\n", i);
        printf("Enter employee id : ");
        scanf("%d", &id);
        temp = create(id);
        i++;
        head = temp;
        last = temp;
    }
    while (i <= n)
    {
        printf("---------------Enter Employee - %d details---------------\n", i);
        insertAtEnd();
        i++;
    }
    printf("\nSuccessfully updated the DLL\n");
}
void displayDLL()
{
    Node *temp = head;
    printf("\n%-10s%-15s%-13s%s\n", "Emp id", "Emp_mobileno", "Emp sal", "Emp dept");
    while (temp != NULL)
    {
        printf("%-10d%-15d%-13.2f%s\n", temp->emp_id, temp->emp_mobileno, temp->emp_sal, temp->emp_dept);
        temp = temp->next;
    }
    printf("\n");
}
void del_main()
{
    free(head);
    head = NULL;
    last = NULL;
}
void deleteaAtEnd()
{
    if (last->prev != NULL)
    {
        last = last->prev;
        free(last->next);
        last->next = NULL;
    }
    else
        del_main();
    count--;
    printf("\nDeleted successfully\n");
}
void deleteAtFront()
{
    if (head->next != NULL)
    {
        head = head->next;
        free(head->prev);
        head->prev = NULL;
    }
    else
        del_main();
    count--;
    printf("\nDeleted successfully\n");
}
void insertAtFront()
{
    int id;
    printf("Enter employee id : ");
    scanf("%d", &id);
    fflush(stdin);
    if (searchNode(id) != NULL)
    {
        printf("\nEmployee already exists in DLL\n");
    }
    else
    {
        Node *temp = create(id);
        head->prev = temp;
        temp = head;
        head = head->prev;
        head->next = temp;
        printf("\nSuccessfully updated the DLL\n");
    }
}
void insert()
{
    int id;
    printf("Enter employee id after which you want to insert : ");
    scanf("%d", &id);
    fflush(stdin);
    Node *temp = searchNode(id);
    if (temp == NULL)
    {
        printf("\nEmployee id entered doesn't exist in DLL\n");
    }
    else
    {
        printf("Enter employee id you want to insert : ");
        scanf("%d", &id);
        if (searchNode(id) != NULL)
        {
            printf("\nEmployee already present in DLL\n");
        }
        else
        {
            Node *temp1 = create(id);
            if (temp->next != NULL)
            {
                temp1->next = temp->next;
                temp->next = temp1;
                temp1->prev = temp;
                temp1->next->prev = temp1;
            }
            else
            {
                temp->next = temp1;
                temp1->prev = temp;
            }
        }
    }
    printf("Successfully updated the DLL\n");
}
void delete ()
{
    int emp_id;
    printf("Enter employee id you want to delete: ");
    scanf("%d", &emp_id);
    Node *temp = searchNode(emp_id);
    if (temp == NULL)
    {
        printf("Employee id entered doesn't exist in DLL\n");
    }
    else
    {
        if (temp->next == NULL)
        {
            deleteaAtEnd();
        }
        else if (temp->prev == NULL)
        {
            deleteAtFront();
        }
        else
        {
            temp->prev->next = temp->next;
            temp->next->prev = temp->prev;
            free(temp);
        }
        count--;
        printf("\nDeleted successfully\n");
    }
}

void finish()
{
    Node *temp;
    while (head != NULL)
    {
        temp = head;
        head = head->next;
        free(temp);
    }
    head = NULL;
    last = NULL;
}

void todo(int option)
{
    switch (option)
    {
    case 1:
        add();
        break;
    case 2:
        printf("\nTotal members in DLL is %d\n", count);
        break;
    case 3:
        if (!count)
            printf("\nThere are no employees in DLL\n");
        else
            displayDLL();
        break;
    case 4:
        if (!count)
            printf("\nThere are no employees in DLL\n");
        else
            insertAtFront();
        break;
    case 5:
        if (!count)
            printf("\nThere are no employees in DLL\n");
        else
        {
            insertAtEnd();
            printf("\nSuccessfully updated the DLL\n");
        }
        break;
    case 6:
        if (!count)
            printf("\nThere are no employees in DLL\n");
        else
            insert();
        break;
    case 7:
        if (!count)
            printf("\nThere are no employees in DLL to delete\n");
        else
            deleteAtFront();
        break;
    case 8:
        if (!count)
            printf("\nThere are no employees in DLL to delete\n");
        else
            deleteaAtEnd();
        break;
    case 9:
        if (!count)
            printf("\n\nThere are no employees in DLL to delete\n\n");
        else
            delete ();
        break;
    case 10:
        finish();
        printf("\n\n------------------------Program ends------------------------\n\n");
        break;
    default:
        printf("\nEnter a valid option !!\n");
    }
}
void operations()
{
    int option;
    do
    {
        printf("\n1-> Add members\n"
               "2->  Count of nodes in DLL\n"
               "3->  Display Employee data in DLL\n"
               "4->  Insert Employee at Front of the DLL\n"
               "5->  Insert Employee at End of the DLL\n"
               "6->  Insert Employee at a specific position in DLL\n"
               "7->  delete Employee at Front of the DLL\n"
               "8->  delete Employee at End of the DLL\n"
               "9->  delete Employee at a specific position in DLL\n"
               "10-> Exit\n");
        printf("\nEnter your option: ");
        scanf("%d", &option);
        todo(option);
    } while (option != 10);
}
int main()
{
    printf("------------------------Program starts------------------------\n\n");
    operations();
    return 0;
}
