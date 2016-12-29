# Fractional-Knapsack
#include<iostream>
using namespace std;
float w[10],p[10],pw[10];
int partition(float ar[],int pin,int r)
{
	int i,j;
	float pivot,temp; 
	pivot=ar[r-1];
	i=pin-1;
	
	for(j=pin;j<r-1;j++)
	{
		if(pivot<ar[j])
		{
			i=i+1;
			temp=ar[i];
			ar[i]=ar[j];
			ar[j]=temp;
			
			temp=w[i];
			w[i]=w[j];
			w[j]=temp;
			
			temp=p[i];
			p[i]=p[j];
			p[j]=temp;
			
		}
	}
    temp=ar[i+1];
	ar[i+1]=ar[r-1];
	ar[r-1]=temp;
	
	temp=w[i+1];
	w[i+1]=w[r-1];
	w[r-1]=temp;
	
	temp=p[i+1];
	p[i+1]=p[r-1];
	p[r-1]=temp;
return i+1;
}

void sort(float ar[],int pin,int r)
{   int q;
	if(pin<r)
	{
		q=partition(ar,pin,r);
		sort(ar,pin,q);
		sort(ar,q+1,r);
	}
}

float knapsac(float pw[],float p[],float w[],float cap)
{
	float wt=0.0f,profit=0.0f,diff;
	int i=0;
	while(wt<=cap)
	{   
	   
		if(w[i]<cap)
		{
			diff=cap-wt;
			if(diff<w[i])
			profit=profit+(diff*pw[i]);
			else
			profit=profit+p[i];
		//	cout<<"Profit becomes "<<profit<<endl;
			wt=wt+w[i];
		}
		i++;
	}
	return profit;
}

int main()
{
	int n,i;
	float x,cap,profit;
	cout<<"Enter the no. of objects "<<endl;
	cin>>n;
	cout<<"Enter the weight and profit of objects "<<endl;
	for(i=0;i<n;i++)
	{
		cout<<"Weight["<<i<<"]: ";
		cin>>w[i];
		cout<<"Profit["<<i<<"]:";
		cin>>p[i];
		x=p[i]/w[i];
		pw[i]=x;
		cout<<"Profit per Weight is "<<pw[i]<<endl;
	}
	cout<<"Enter the capacity of the bag "<<endl;
	cin>>cap;
	sort(pw,0,n);
	profit=knapsac(pw,p,w,cap);
    cout<<"The profit is "<<profit;
	return 0;
}
