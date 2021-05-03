//updated 8:30pm 2/1/18
#include<fstream>
#include<iostream>
#include<stdio.h>
#include<iomanip>       //setw function
#include<stdlib.h>      //clear screen function
#include<process.h>     //for exit function
#include<cstring>       //for string functions
using namespace std;
void displaytable();
void displayelem(char []);
int main()
{
    char atm[4];
    char ch='y'; //for choice
    while(ch=='y'||ch=='Y')
   {
        system("cls");
        cout<<setw(40)<<"Periodic Table\n";
        displaytable();
        cout<<"\nEnter atomic number(1-118): ";
        gets(atm);
        displayelem(atm);
//        system("PAUSE");
        cout<<"Do you want to try search another element?(y/n): ";
        cin>>ch;
        if(ch=='y'||ch=='Y')
        {
            cout<<"Enter atomic number(1-118): ";
            gets(atm);
        }
   }


    return 0;
}
void displayelem(char atm[])
{
    ifstream infile;
    char atomic_no[10],symbol[10],fullname[10],line[20],atomic_weight[10],density[10],melt[10],boil[10],Heat_Capacity[10],Electronegativity[10],Qty_OE[10];

	int flag=0;
    infile.open("elements2.txt");
    if(!infile)
    {
        cout<<"Error opening elements.txt";
        system("PAUSE");
        exit(0);
    }

    while(infile.eof()==0)
    {
        infile>>line;
        if(strcmpi(line,atm)==0)
            {
				flag=1;
                infile>>line;
                strcpy(symbol,line);
                cout<<"Symbol : "<<symbol<<endl;
                infile>>line;
                strcpy(fullname,line);
                cout<<"Fullname : "<<fullname<<endl;
                infile>>line;
                strcpy(atomic_weight,line);
                cout<<"Atomic weight: "<<atomic_weight<<endl;
                infile>>line;
                strcpy(density,line);
                cout<<"Density (g/cm3) :"<<density<<endl;
                infile>>line;
                strcpy(melt,line);
                cout<<"Melting point (K): "<<melt<<endl;
                infile>>line;
                strcpy(boil,line);
                cout<<"Boiling point (K): "<<boil<<endl;
                infile>>line;
                strcpy(Heat_Capacity,line);
                cout<<"Heat capacity (J/g*K): "<<Heat_Capacity<<endl;
                infile>>line;
                strcpy(Electronegativity,line);
                cout<<"Electro-negativity : "<<Electronegativity<<endl;
                infile>>line;
                strcpy(Qty_OE,line);
                cout<<"Quantity on Earth (mg/kg): "<<Qty_OE<<endl;
                break;
            }

    }
	if(flag==0)
	{
		cout<<"\nThere is no element found with this atomic number\n";
	}
    infile.close();
}
void displaytable() //displaying periodic table
{
    ifstream ifile;
	char s[100];
	ifile.open("table.txt");
    if(!ifile)
	{
		cout<<"Error in opening table.txt";
		system("PAUSE");
		exit(0);
	}
	while(ifile.eof()==0)
    {
        ifile.getline(s,61,'\n');
        cout<<setw(65)<<s<<endl;
    }
	cout<<"\n";
	ifile.close();
}
