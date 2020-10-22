/*Bubble sort using c++
* iterates from first element to last, compares every element
*
*/

#include<iostream>
using namespace std;
#define l "\n"
int i,j;
int *temp;
void display(int a[],int n){
	for( i=0;i<n;i++)
		cout<<a[i]<<" ";
	cout<<l<<l;
}

void swap(int *x,int *y){
	*temp=*x;
	*x=*y;
	*y=*temp;
}

void Bubblesort(int a[],int n){
	for( i=0;i<n-1;i++){
		for( j=i+1;j<n;j++){
			if(a[i]>a[j])
			swap(a[i],a[j]);
		}
	}
	cout<<"After sorting elements of array are: ";
	display(a,n);
}

void intialize(int n){
	int a[n];
	for( i=0;i<n;i++){
		cout<<"Enter element-"<<i+1<<": ";
		cin>>a[i];
	}
	system("cls");
	cout<<"Before sorting elements of array are: ";
	display(a,n);
	Bubblesort(a,n);
}

int main(){
	int n;
	cout<<"Enter size of the array: ";
	cin>>n;
	cout<<l;
	intialize(n);
	return 0;
}
