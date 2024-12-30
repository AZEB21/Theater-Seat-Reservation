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

// Function to convert Gregorian date to Ethiopian date
void convertToEthiopianDate(int year, int month, int day, int& ethYear, int& ethMonth, int& ethDay) {
    ethYear = year - ETHIOPIAN_YEAR_OFFSET;
    ethMonth = (month >= 9) ? (month - 8) : (month + 4);
    ethDay = day;
    if (month < 9) ethYear--; // Adjust year if before Ethiopian New Year
}

// Main reservation function
void reserveSeat() {
    cout << "\nWelcome to Ambassador Theater!\n";

    // Select movie
    cout << "\nAvailable Movies:\n";
    for (size_t i = 0; i < movies.size(); ++i) {
        cout << i + 1 << ". " << movies[i] << " (" << genres[i] << ")\n   " << trailers[i] << "\n";
    }
    int movieIndex;
    cout << "Select a movie (1-" << movies.size() << "): ";
    cin >> movieIndex;
    if (movieIndex < 1 || movieIndex > movies.size()) {
        cout << "Invalid movie selection.\n";
        return;
    }
string selectedMovie = movies[movieIndex - 1];

    // Select hall
    int hall;
    cout << "\nSelect hall (1-3): ";
    cin >> hall;
    if (hall < 1  hall > 3) {
        cout << "Invalid hall number.\n";
        return;
    }
    hall -= 1;

    displaySeats(hall);

    // Select row
    int row;
    cout << "Select row (1-" << theater[hall].size() << "): ";
    cin >> row;
    if (row < 1  row > theater[hall].size()) {
        cout << "Invalid row number.\n";
        return;
    }
    row -= 1;

    // Select seat
    int seat;
    cout << "Select seat (1-" << theater[hall][row].size() << "): ";
    cin >> seat;
    if (seat < 1  seat > theater[hall][row].size()) {
        cout << "Invalid seat number.\n";
        return;
    }
    seat -= 1;

    if (theater[hall][row][seat]) {
        cout << "Sorry, this seat is already reserved.\n";
        return;
    }

    // Reserve the seat
    theater[hall][row][seat] = true;

    // Select ticket type
    string type;
    double price;
    cout << "\nSelect ticket type (CBIP, Regular, Premium): ";
    cin >> type;
    if (type == "CBIP") {
        price = 20.00;
    } else if (type == "Regular") {
        price = 5.00;
    } else if (type == "Premium") {
        price = 15.00;
    } else {
        cout << "Invalid ticket type.\n";
        return;
    }

    // Select showtime
    cout << "\nAvailable Showtimes:\n";
    for (size_t i = 0; i < showtimes.size(); ++i) {
        cout << i + 1 << ". " << showtimes[i] << "\n";
    }

int showtimeIndex;
    cout << "Select a showtime (1-" << showtimes.size() << "): ";
    cin >> showtimeIndex;
    if (showtimeIndex < 1  showtimeIndex > showtimes.size()) {
        cout << "Invalid showtime selection.\n";
        return;
    }
      
