#include <iostream>
#include <fstream>
#include <string>
#include <vector>

using namespace std;

struct Train {
 string name;
 int distance;
 int price;
};

struct Ticket {
 string destination;
 string departure;
 string date;
 string train;
 string name;
 int age;
 int price;
};

vector<Train> trains;
vector<Ticket> tickets;

void loadTrains() {
 ifstream file("trains.txt");
 string name;
 int distance, price;
 while (file >> name >> distance >> price) {
  Train train = {name, distance, price};
  trains.push_back(train);
 }
}

void displayTrains() {
 cout << "Select a train:" << endl;
 for (int i = 0; i < trains.size(); i++) {
  cout << i + 1 << ". " << trains[i].name << endl;
 }
}

void bookTicket() {
 Ticket ticket;
 cout << "Enter destination: ";
 cin >> ticket.destination;
 cout << "Enter departure: ";
 cin >> ticket.departure;
 cout << "Enter date (DD-MM-YYYY): ";
 cin >> ticket.date;
 displayTrains();
 int choice;
 cin >> choice;
 ticket.train = trains[choice - 1].name;
 cout << "Enter name: ";
 cin >> ticket.name;
 cout << "Enter age: ";
 cin >> ticket.age;
 ticket.price = trains[choice - 1].price;
 tickets.push_back(ticket);
}

void displayTickets() {
 cout << "Booked Tickets:" << endl;
 for (int i = 0; i < tickets.size(); i++) {
  cout << "Destination: " << tickets[i].destination << endl;
  cout << "Departure: " << tickets[i].departure << endl;
  cout << "Date: " << tickets[i].date << endl;
  cout << "Train: " << tickets[i].train << endl;
  cout << "Name: " << tickets[i].name << endl;
  cout << "Age: " << tickets[i].age << endl;
  cout << "Price: " << tickets[i].price << endl;
  cout << "------------------------" << endl;
 }
}

int main() {
 loadTrains();
 while (true) {
  cout << "1. Book Ticket" << endl;
  cout << "2. Display Tickets" << endl;
  cout << "3. Exit" << endl;
  int choice;
  cin >> choice;
  switch (choice) {
   case 1:
    bookTicket();
    break;
   case 2:
    displayTickets();
    break;
   case 3:
    return 0;
  }
 }
}
