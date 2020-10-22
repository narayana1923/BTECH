#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct Node{
    char name[50];
    char rollnumber[11];
    struct Node* next;
}node;
node* head;
node* first;
node* last;
void intialization_of_heads(){
    printf("Enter the name of the readers club head : ");
    gets(first->name);
    printf("Enter the roll number of the readers club head : ");
    gets(first->rollnumber);
    printf("Enter the name of the in-charge of readers club : ");
    gets(last->name);
    printf("Enter the roll number of the in-charge of readers club : ");
    gets(last->rollnumber);
    first->next=last;
    last->next=NULL;
    head=first;
}

int total_members(){
	int n=0;
	node* temp=head;
	while(temp!=NULL){
		temp=temp->next;
		n++;
	}
	return n;
}

node* searchNode(char rollnumber[]){
				node* temp = NULL;
				node* ptr=head;
				while(ptr!=NULL){
					if(strcasecmp(ptr->rollnumber,rollnumber)==0){
						temp=ptr;
						break;
					}
					ptr=ptr->next;
				}
				return temp;
			}
void add(){
	char rollnumber[11];
	fflush(stdin);
	printf("Enter the roll number of person : ");
	gets(rollnumber);
	if(searchNode(rollnumber)!=NULL){
		printf("\nStudent is already present in readers club\n\n");
	}
	else{
		char name[50];
		printf("Enter the name of person : ");
		gets(name);
		if(head==NULL){
			strcpy(first->name,name);
			strcpy(first->rollnumber,rollnumber);
			head=first;
			head->next=NULL;
			printf("\nSuccessfully added the student to readers club\n");
			return;
		}
		if(head->next==NULL){
			last=malloc(sizeof(node));
			strcpy(last->name,name);
			strcpy(last->rollnumber,rollnumber);
			head->next=last;
			printf("\nSuccessfully added the student to readers club\n");
			return;
		}
		node* temp=head;
		while(temp->next!=last) temp=temp->next;
		temp->next=malloc(sizeof(node));
		strcpy(temp->next->name,name);
		strcpy(temp->next->rollnumber,rollnumber);
		temp->next->next=last;
		printf("\nSuccessfully added the students to readers club\n");
		}

}

		void sort(){
			char a[11];
			char b[50];
			node* temp=head;
			while(temp->next!=NULL){
				node* min=temp;
				node* temp1=temp->next;
				while(temp1!=NULL){
					if(strcasecmp(temp1->name,min->name)<0){
						min=temp1;
					}
					temp1=temp1->next;
				}
				strcpy(a,min->name);
				strcpy(b,min->rollnumber);
				strcpy(min->name,temp->name);
				strcpy(min->rollnumber,temp->rollnumber);
				strcpy(temp->name,a);
				strcpy(temp->rollnumber,b);
				temp=temp->next;
			}
		}

		void delet(){
			if(total_members()==0){
				printf("\nThere are no members in readers club\n");
			}
			else{
				char rollnumber[11];
				printf("Enter the roll number of student you want to delete : ");
				gets(rollnumber);
				if(searchNode(rollnumber)==NULL){
					printf("\nThere is no one in the readers club with the roll number %s \n",rollnumber);
					return;
				}
				sort(head);
				if(strcasecmp(head->rollnumber,rollnumber)==0){
					/*head=head->next;
					free(last);*/
					//node* temp=head;
					head=head->next;
					//ree(temp);
					printf("\nThe student you entered has been removed form readers club\n");
					return;
				}
				node* temp=head;
				node* prev=temp;
				while( temp->next!=NULL && strcasecmp(temp->rollnumber,rollnumber)!=0){
					prev=temp;
					temp=temp->next;
					if(strcasecmp(temp->rollnumber,rollnumber)==0) break;
				}
				if(strcasecmp(temp->rollnumber,rollnumber)==0){
					prev->next=temp->next;
					//temp->next=NULL;
					free(temp->next);
				}
				printf("\nThe student you entered has been removed form readers club\n");
			}
		}

		void display_members(){
			node* temp=head;
			while(temp!=NULL){
				printf("%-30s%s\n",temp->name,temp->rollnumber);
				temp=temp->next;
			}
			printf("\n");
		}

		void display_reverse(node* head){
			if(head->next!=NULL){
				display_reverse(head->next);
			}
			printf("%-30s%s\n", head->name, head->rollnumber);
		}

		void todo(int option){
			switch(option){
						case 1:
							add( );
							break;
						case 2:
							delet();
							break;
						case 3:
							printf("\nTotal number of members in readers club are %d \n",total_members(head));
							break;
						case 4:
							if(total_members()==0) printf("\nThere are no members in readers club\n");
							else{printf("\n%-30s%s\n","Name","Roll Number");
							display_members();}
							break;
						case 5:
							if(total_members()==0) printf("\nThere are no members in readers club\n");
							else{printf("\n%-30s%s\n","Name","Roll Number");
							display_reverse(head);}
							printf("\n");
							break;
						case 6:
							if(total_members()==0) printf("\nThere are no members in readers club to sort\n");
							else{sort();
							printf("\nSorted the list successfully\n");}
							break;
						case 7:
							printf("\nProgram ended!!\n");
							break;
						default:
							printf("\nInvalid option, please try again\n");

					}
		}

		void operation(){
			int option;
			do{
				printf("\n1-> Add a member\n"
					  "2-> Delete a members\n"
					  "3-> Count of students in readers club\n"
					  "4-> Display All members in readers club\n"
					   "5-> Display all the members in reverse order\n"
					   "6-> sort the list\n"
					   "7-> To exit Enter 7 or any number >7\n");
				printf("\nEnter your option: ");
				scanf("%d",&option);
				fflush(stdin);
				todo(option);
			}while(option!=7);
		}

int main() {
	setbuf(stdout, NULL);
	first=(node*) malloc(sizeof(node));
	last=(node*) malloc(sizeof(node));
	intialization_of_heads();
	operation();
	return 0;
}