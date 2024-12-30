#include <iostream>
#include <vector>
#include <iomanip>
#include <string>
using namespace std;

// Ethiopian calendar year offset (difference from Gregorian calendar)
const int ETHIOPIAN_YEAR_OFFSET = 8;

// Theater layout: 3 halls, each with rows and seats
vector<vector<vector<bool>>> theater = {
    {{false, false, false, false, false, false, false, false, false, false},
     {false, false, false, false, false, false, false, false, false, false}}, // Hall 1

    {{false, false, false, false, false, false, false, false},
     {false, false, false, false, false, false, false, false}}, // Hall 2

    {{false, false, false, false, false, false, false, false, false, false, false, false},
     {false, false, false, false, false, false, false, false, false, false, false, false}} // Hall 3
};

// Predefined movies with genres and trailers
vector<string> movies = {"The Great Romance", "Haunted Thriller", "Action Heroes"};
vector<string> genres = {"Romance", "Thriller", "Action"};
vector<string> trailers = {
    "Trailer: A love story that transcends time.",
    "Trailer: A haunted house you’ll never escape from.",
    "Trailer: Explosions, car chases, and heroic battles!"
};

// Predefined showtimes
vector<string> showtimes = {"1:00 PM", "4:00 PM", "7:30 PM"};

// Function to display seats for a given hall
void displaySeats(int hall) {
    cout << "\nHall " << hall + 1 << " Layout:\n";
    for (size_t row = 0; row < theater[hall].size(); ++row) {
        cout << "Row " << row + 1 << ": ";
        for (size_t seat = 0; seat < theater[hall][row].size(); ++seat) {
            cout << (theater[hall][row][seat] ? "X " : "_ ");
        }
        cout << endl;
    }
}


      
