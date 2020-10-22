#include<stdio.h>
#include<string.h>
int i=0;
int unodr_linear_search(char b[],int n,char a[n][20]){
    for(i=0;i<n;i++){
        if(strcasecmp(a[i],b)==0) return 1;
    }
    return 0;
}
void intialization(int n,char a[n][20]){
    printf("Enter Student roll numbers separated by space: ");
    for(i=0;i<n;i++) scanf("%s",a[i]);
}
int main(){
    int n;
    printf("Enter number of students: ");
    scanf("%d",&n);
    fflush(stdin);
    char b[20];
    char a[n][20];
    intialization(n,a);
    printf("Enter the roll number you want to check: ");
    scanf("%s",b);
    printf("Student with Roll number %s %s for Placement training",b,(unodr_linear_search(b,n,a))? " attended": " not attended");
    return 0;
}
