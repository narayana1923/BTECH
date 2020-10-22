#include<iostream>
#include<algorithm>
using namespace std;
int i=0;
const char line='\n';
int unodr_linear_search(string a[],string b,int n){
    for(i=0;i<n;i++){
        if(a[i].compare(b)==0) return 1;
    }
    return 0;
}
void intialization(string a[],int n){
    cout<<"Enter Student roll numbers separated by space: ";
    for(i=0;i<n;i++) {
        cin>>a[i];
        transform(a[i].begin(), a[i].end(), a[i].begin(), ::toupper);
    }
    system("cls");
}
int main(){
    int n;
    cout<<"Enter number of students: ";
    cin>>n;
    string a[n];
    intialization(a,n);
    string b;
    cout<<"Enter the roll number you want to check: ";
    cin>>b;
    transform(b.begin(), b.end(), b.begin(), ::toupper);
    cout<<"Student with Roll number "<<b<<((unodr_linear_search(a,b,n))? " attended": " not attended")<<" for Placement training";
    return 0;
}
