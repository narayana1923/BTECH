#include <stdio.h>
int i=0,j=0,temp=0;
void display(int a[],int n){
    for(i=0;i<n;i++) printf("%d ",a[i]);
    printf("\n");
}
void insertion_sort(int a[],int n){
    for(i=n-2;i>=0;i--){
      temp=a[i];
      for(j=i;j<n-1 && a[j+1]<temp;j++) a[j]=a[j+1];
      a[j]=temp;
    }
}
void intialization(int a[],int n){
    printf("Enter array elements seperated by space: ");
    for(int i=0;i<n;i++) scanf("%d",&a[i]);
    printf("\n");
}
int main(){
    int n;
    printf("Enter number of elements of the array: ");
    scanf("%d",&n);
    printf("\n");
    int a[n];
    intialization(a,n);
    printf("Before sorting the array elements are: ");
    display(a,n);
    printf("\n");
    insertion_sort(a,n);
    printf("After sorting the array elements are: ");
    display(a,n);
    return 0;
}
