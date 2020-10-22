#include<iostream>
const char line= '\n';
using namespace std;
int i,j,temp=0;
void intialization(int [],int);
void display(int [],int);
void selection_sort(int [],int);
void swap(int* ,int*);
int main(){
    int n;
    cout<<"Enter size of array: ";
    cin>>n;
    cout<<line;
    int a[n];
    intialization(a,n);
    cout<<"Array elements before sorting: ";
    display(a,n);
    selection_sort(a,n);
    cout<<"Array elements after sorting: ";
    display(a,n);
    return 0;
}

void intialization(int a[],int n){
    cout<<"Enter array elements separated by space: ";
    for(i=0;i<n;i++) cin>>a[i];
    cout<<line;
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
    for(i=0;i<n;i++) cout<<a[i]<<" ";
    cout<<line;
}
