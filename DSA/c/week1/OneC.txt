#include<stdio.h>
int i,j,temp=0;
void intialization(int [],int);
void display(int [],int);
void selection_sort(int [],int);
void swap(int* ,int*);
int main(){
    int n;
    printf("Enter size of array: ");
    scanf("%d",&n);
    printf("\n");
    int a[n];
    intialization(a,n);
    printf("Array elements before sorting: ");
    display(a,n);
    selection_sort(a,n);
    printf("Array elements after sorting: ");
    display(a,n);
    return 0;
}

void intialization(int a[],int n){
    printf("Enter array elements separated by space: ");
    for(i=0;i<n;i++) scanf("%d",&a[i]);
    printf("\n");
}
void swap(int* x,int* y){
    temp=*x;
    *x=*y;
    *y=temp;
}
void selection_sort(int a[],int n){
    int min=0;
    for(i=0;i<n;i++){
            min=i;
        for(j=i+1;j<n;j++)
            if(a[j]<a[min])
                min=j;
        swap(&a[i],&a[min]);
    }
}

void display(int a[],int n){
    for(i=0;i<n;i++) printf("%d ",a[i]);
    printf("\n");
}
