Theater Reservation System
This C++ program simulates a theater reservation system that allows users to reserve seats for movies. It supports seat selection, ticket types, showtimes, and Ethiopian date conversion. The program is designed to provide a user-friendly interface for managing movie reservations.

Features
Movie Selection: Choose from a list of available movies with genres and trailers.

Seat Reservation: Select seats from a predefined theater layout.

Ticket Types: Choose between CBIP, Regular, and Premium ticket types with different prices.

Showtimes: Select from available showtimes for the chosen movie.

Ethiopian Date Conversion: Converts the Gregorian date to the Ethiopian calendar for ticket generation.

Code Structure
The program is structured into the following components:

Theater Layout: A 3D vector representing the seating arrangement for three halls.

Movie Data: Vectors storing movie names, genres, and trailers.

Showtimes: A vector of available showtimes.

Functions:

displaySeats(int hall): Displays the seating layout for a selected hall.

convertToEthiopianDate(int year, int month, int day, int& ethYear, int& ethMonth, int& ethDay): Converts Gregorian dates to Ethiopian dates.

reserveSeat(): Handles the reservation process, including seat selection, ticket type, and showtime.

Example Output

Welcome to Ambassador Theater!

Available Movies:
1. The Great Romance (Romance)
   Trailer: A love story that transcends time.
2. Haunted Thriller (Thriller)
   Trailer: A haunted house you’ll never escape from.
3. Action Heroes (Action)
   Trailer: Explosions, car chases, and heroic battles!
4. Tropic Thunder (comedy)
   Trailer: humorously teases a chaotic jungle adventure.
5. Spirited away (Animation)
   Trailer: captures a young girl's magical adventure.
Select a movie (1-5): 1

Select hall (1-3): 1

Hall 1 Layout:
Row 1: _ _ _ _ _ _ _ _ _ _ 
Row 2: _ _ _ _ _ _ _ _ _ _ 
Select row (1-2): 1
Select seat (1-10): 5

Select ticket type (CBIP, Regular, Premium): Premium

Available Showtimes:
1. 1:00 PM
2. 4:00 PM
3. 7:30 PM
Select a showtime (1-3): 2

Enter today's date:
Year (e.g., 2024): 2024
Month (1-12): 10
Day (1-31): 15

--- Your Ticket ---
Ambassador Theater
Movie: The Great Romance
Type: Premium
Price: $15.00
Hall: 1
Row: 1
Seat: 5
Showtime: 4:00 PM
Date: 2016/2/15 (Ethiopian Calendar)
-------------------

Would you like to reserve another ticket? (y/n): n
Thank you for using Ambassador Theater's reservation system!
