#include <iostream>
#define line "\n"
using namespace std;
int i=0,j=0,temp=0;
void display(int a[],int n){
    for(i=0;i<n;i++) cout<<a[i]<<" ";
    cout<<line;
}
void insertion_sort(int a[],int n){
    for(i=n-2;i>=0;i--){
      temp=a[i];
      for(j=i;j<n-1 && a[j+1]<temp;j++) a[j]=a[j+1];
      a[j]=temp;
    }
}
void intialization(int a[],int n){
    cout<<"Enter array elements seperated by space: ";
    for(int i=0;i<n;i++) cin>>a[i];
    cout<<line;
}
int main(){
    int n;
    cout<<"Enter number of elements of the array: ";
    cin>>n;
    cout<<line;
    int a[n];
    intialization(a,n);
    cout<<"Before sorting the array elements are: ";
    display(a,n);
    cout<<line;
    insertion_sort(a,n);
    cout<<"After sorting the array elements are: ";
    display(a,n);
    return 0;
}
