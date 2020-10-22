#include <iostream>
#include <algorithm>
using namespace std;
const char line='\n';
int i,j,k;
void intialization(string a[],int n){
    cout<<"Enter student roll numbers separated by space : ";
    for (i=0;i<n;i++) cin>>a[i];
    cout<<line;
}
void shell_sort(string a[],int n){
    string temp;
    for(i=0;i<n;i++) transform(a[i].begin(),a[i].end(),a[i].begin(),::toupper);
    for(i=n/2;i>0;i/=2){
        for(j=i;j<n;j++){
            temp=a[j];
            for(k=j;k>=i && temp.compare(a[k-i])<0;k-=i) a[k]=a[k-i];
            a[k]=temp;
        }
    }
}
int binary_search(string a[],int n,string b){
    int low=0,mid=0,high=n-1;
    while(low<=high){
        mid=(low+high)/2;
        /*if(b.compare(a[low])<0) return 0;
        else if(b.compare(a[high])>0) return 0;
        else*/
        if(b.compare(a[mid])==0) return 1;
        else if(b.compare(a[mid])>0) low=mid+1;
        else if(b.compare(a[mid])<0) high=mid-1;
    }
    return 0;
}
int main(){
    int n;
    cout<<"Enter number of students: ";
    cin>>n;
    string a[n];
    intialization(a,n);
    shell_sort(a,n);
    string b;
    cout<<"Enter the roll number you want to search: ";
    cin>>b;
    transform(b.begin(),b.end(),b.begin(),::toupper);
    binary_search(a,n,b);
    cout<<"----------------------using Non-Recursive Binary Search----------------------------"<<line;
    cout<<"The student with roll number "<<b<<((binary_search(a,n,b)? " ":" not "))<<"attended placement training"<<line;
    return 0;
}
