#include <stdio.h>
#include <string.h>
int i,j,k;
void intialization(int n,char a[n][20]){
    printf("Enter student roll numbers separated by space : ");
    for (i=0;i<n;i++) scanf("%s",a[i]);
    printf("\n");
}
void shell_sort(int n,char a[n][20]){
    char temp[20];
    for(i=n/2;i>0;i/=2){
        for(j=i;j<n;j++){
            strcpy(temp,a[j]);
            for(k=j;k>=i && strcasecmp(temp,a[k-i])<0;k-=i) 
                strcpy(a[k],a[k-i]);
            strcpy(a[k],temp);
        }
    }
}
int binary_search(int n,char a[n][20],char b[]){
    int low=0,mid=0,high=n-1;
    while(low<=high){
        mid=(low+high)/2;
        if(strcasecmp(b,a[mid])==0) return 1;
        else if(strcasecmp(b,a[mid])>0) low=mid+1;
        else if(strcasecmp(b,a[mid])<0) high=mid-1;
    }
    return 0;
}
int main(){
    int n;
    printf("Enter number of students: ");
    scanf("%d",&n);
    char a[n][20];
    intialization(n,a);
    shell_sort(n,a);
    char b[20];
    printf("Enter the roll number you want to search: ");
    scanf("%s",b);
    printf("----------------------using Non-Recursive Binary Search----------------------------\n");
    printf("The student with roll number %s%sattended placement training",b,(binary_search(n,a,b)? " ":" not "));
    return 0;
}
