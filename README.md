# Snack-Machine
Vending machine simulator

//Snack Machine So Far
#include <iostream>
#include <string>
#include <iomanip>
using namespace std;


//Structure
struct SnackData
{
  string name;
  double cost;
  int inventory;
  int option;
};


//Prototypes
void machineDisplay(SnackData);
void machineEndDisplay(SnackData snack);

int main()
{
string name;
double cost, moneyin, changedue, totalmoney, tempmoney;
int inventory, choice, i, c;

SnackData snackarray[4]= {{"Oreo cookie package", 0.75, 0, 1}, {"Granola bars", 0.80, 30, 2}, {"Oatmeal raisin cookies", 0.75, 15, 3}, {"Tortilla chips (spicy)", 0.60, 20, 4}};

cout << "Snack Machine" <<endl <<"*************************" <<endl<<endl;


do
{
//Display Menu
for (i=0; i<4; i++)
  {
    machineDisplay(snackarray[i]);
  }
  cout << "5: Quit" <<endl<<endl;

  cout << "Enter an available option (1 through 5): ";
  cin >> c;
  
    while (c<1 || c>5)
    {
      cout << "You entered incorrectly, try again: ";
      cin >> c;
    }

  while (c<5 && c>1 && snackarray[c-1].inventory==0)
  { 
    cout << "You entered incorrectly, try again: ";
    cin >> c;
  }
  
  cout << "Price: $" <<snackarray[c-1].cost<<endl;
  cout << "How much money did you enter?: $";
  cin >> moneyin;
  while (moneyin <= snackarray[c-1].cost || c>5)
  {
    cout << "You entered too little, try again: ";
    cin >> moneyin;
  }
  cout << "Vending..." << endl;
  changedue = moneyin-snackarray[c-1].cost;
  cout << "Change due: $" << changedue <<endl;
  tempmoney = moneyin-changedue;
  totalmoney = totalmoney+tempmoney;
      
  snackarray[c-1].inventory= snackarray[c-1].inventory-1;
} while (c!=5);

cout << "Come back soon" << endl<<endl<<endl;

cout << "Total money collected: $" << totalmoney <<endl;
cout << "Remaining inventory... " << endl;


  for (i=0; i<4; i++)
  {
    machineEndDisplay(snackarray[i]);
  }

return 0;
}


//Function for Menu Display
void machineDisplay(SnackData snack)
{
if (snack.inventory!=0)
{
  cout << fixed << showpoint << setprecision(2);
  cout << snack.option<< ": " << snack.name << endl;
  cout << "Cost: $"  << snack.cost << endl<<endl;
}
}

//Function for End Inventory Display
void machineEndDisplay(SnackData snack)
{
  cout << snack.name << ": ";
  cout << snack.inventory <<endl;
}
