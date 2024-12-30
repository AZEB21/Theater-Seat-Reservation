#include <iostream>  
#include <string>  
#include <iomanip>
#include <unistd.h>
#include <limits> // For input validation  
using namespace std;
const int VIP_CAPACITY = 30;  
const int STANDARD_CAPACITY = 70;  
const int TOTAL_SEATS = VIP_CAPACITY + STANDARD_CAPACITY;  

int vipSeats[VIP_CAPACITY] = {0}; // 0 means available, 1 means occupied  
int standardSeats[STANDARD_CAPACITY] = {0};  

// Multidimensional array for patron details  
string patrons[TOTAL_SEATS][5]; // 0: Name, 1: Genre, 2: Age, 3: Unique ID, 4: Section  
int patronSeatNumbers[TOTAL_SEATS];  
int patronCount = 0;  
int main() {  
    int choice;  
    do {  
        system("clear");
        cout << "\n--- Theater Seat Reservation System ---\n";  
        cout << "1. Reserve VIP Seat\n";  
        cout << "2. Reserve Standard Seat\n";  
        cout << "3. Display Occupancy Status\n";  
        cout << "4. Search Patron by Name\n";  
        cout << "5. Exit\n";  
        cout << "Enter your choice: ";  

        // Input validation for choice  
        while (!(cin >> choice) || choice < 1 || choice > 5) {  
            cout << "Invalid choice. Please enter a number between 1 and 5: ";  
            cin.clear(); // Clear error state  
            cin.ignore(numeric_limits<streamsize>::max(), '\n'); // Discard invalid input  
        }  

        if (choice == 1 || choice == 2) {  
            string name, genre, section;  
            int age;  
            int seatNumber = -1;  
            int* seatArray;  
            int seatLimit, offset;  

            // Determine which section to reserve  
            if (choice == 1) {  
                seatArray = vipSeats;  
                seatLimit = VIP_CAPACITY;  
                offset = 1; // Seat numbers start from 1  
                section = "VIP";  
            } else {  
                seatArray = standardSeats;  
                seatLimit = STANDARD_CAPACITY;  
                offset = 31; // Seat numbers start from 31  
                section = "Standard";  
            }  

            // Find the first available seat in the requested section  
            for (int i = 0; i < seatLimit; i++) {  
                if (seatArray[i] == 0) { // 0 means available  
                    seatNumber = i + offset; // Calculate actual seat number  
                    seatArray[i] = 1; // Mark seat as occupied  
                    break;  
                }  
            }  

            // If no seats are available in the requested section  
            if (seatNumber == -1) {  
                char choice;  
                cout << "The requested section is full. Would you like to be seated in the other section? (y/n): ";  
                cin >> choice;  

                // Input validation for choice  
                while (choice != 'y' && choice != 'Y' && choice != 'n' && choice != 'N') {  
                    cout << "Invalid input. Please enter 'y' for yes or 'n' for no: ";  
                    cin >> choice;  
                }  

                if (choice == 'y' || choice == 'Y') {  
                    // Switch to the other section  
                    seatArray = (seatArray == vipSeats) ? standardSeats : vipSeats;  
                    seatLimit = (seatArray == vipSeats) ? VIP_CAPACITY : STANDARD_CAPACITY;  
                    offset = (seatArray == vipSeats) ? 1 : 31;  
                    section = (seatArray == vipSeats) ? "VIP" : "Standard";  

                    for (int i = 0; i < seatLimit; i++) {  
                        if (seatArray[i] == 0) {  
                            seatNumber = i + offset;  
                            seatArray[i] = 1;  
                            break;  
                        }  
                    }  

                    if (seatNumber == -1) {  
                        cout << "No seats available in the other section either.\n";  
                        continue;  
                    }  
                } else {  
                    cout << "No seat assigned.\n";  
                    continue;  
                }  
            }  

            // Collect patron details  
            cout << "Enter your name: ";  
            cin.ignore(); // Clear the newline from previous input  
            getline(cin, name);  
            cout << "Enter your preferred genre: ";  
            getline(cin, genre);  

            // Input validation for age  
            cout << "Enter your age: ";  
            while (!(cin >> age) || age < 0 || age > 120) {  
                cout << "Invalid age. Please enter a valid age (0-120): ";  
                cin.clear(); // Clear error state  
                cin.ignore(numeric_limits<streamsize>::max(), '\n'); // Discard invalid input  
            }  

            // Assign a unique ID  
            int uniqueID = patronCount + 1;  

            // Save patron information  
            patrons[patronCount][0] = name;  
            patrons[patronCount][1] = genre;  
            patrons[patronCount][2] = to_string(age);  
            patrons[patronCount][3] = to_string(uniqueID);  
            patrons[patronCount][4] = section;  
            patronSeatNumbers[patronCount] = seatNumber;  
            patronCount++;  

            // Generate ticket  
            cout << "\n--- Ticket ---\n";  
            cout << "Name: " << name << endl;  
            cout << "Age: " << age << endl;  
            cout << "Genre: " << genre << endl;  
            cout << "Section: " << section << endl;  
            cout << "Seat Number: " << seatNumber << endl;  
            cout << "Unique ID: " << uniqueID << endl;  
            sleep(3);
        } else if (choice == 3) {  
            cout << "\n--- Current Seat Occupancy ---\n";  
            cout << "VIP Seats: \n";  
            for (int i = 0; i < VIP_CAPACITY; i++) {  
                cout << "Seat " << i + 1 << ": " << (vipSeats[i] ? "Occupied" : "Available") << endl;  
            }  

            cout << "\nStandard Seats: \n";  
            for (int i = 0; i < STANDARD_CAPACITY; i++) {  
                cout << "Seat " << i + 31 << ": " << (standardSeats[i] ? "Occupied" : "Available") << endl;  
            } 
            sleep(30);
        } else if (choice == 4) {  
            string searchName;  
            cout << "Enter the name of the patron to search: ";  
            cin.ignore();  
            getline(cin, searchName);  

            bool found = false;  
            for (int i = 0; i < patronCount; i++) {  
                if (patrons[i][0] == searchName) {  
                    found = true;  
                    cout << "\n--- Patron Details ---\n";  
                    cout << "Name: " << patrons[i][0] << endl;  
                    cout << "Age: " << patrons[i][2] << endl;  
                    cout << "Genre: " << patrons[i][1] << endl;  
                    cout << "Section: " << patrons[i][4] << endl;  
                    cout << "Seat Number: " << patronSeatNumbers[i] << endl;  
                    cout << "Unique ID: " << patrons[i][3] << endl;  
                    break;  
                }  
            }  

            if (!found) {  
                cout << "No patron found with the name " << searchName << ".\n";  
            } 
             sleep(3);
        } else if (choice == 5) {  
            cout << "Exiting the system. Goodbye!\n";  
        }  
    } while (choice != 5);  

    return 0;  
}

