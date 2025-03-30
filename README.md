# -Hotel-Booking-System-using-C++
#include <iostream> // Include the input-output stream library
#include <vector> // Include vector for dynamic array storage
using namespace std;

// Class representing a hotel room
class Room {
public:
    int roomNumber; // Room number identifier
    bool isBooked; // Booking status
    string customerName; // Name of the customer who booked the room

    // Constructor to initialize room details
    Room(int number) {
        roomNumber = number;
        isBooked = false; // Room is initially not booked
        customerName = ""; // No customer assigned
    }
};

// Class representing the hotel
class Hotel {
private:
    vector<Room> rooms; // Collection of rooms in the hotel

public:
    // Constructor to initialize hotel with a given number of rooms
    Hotel(int totalRooms) {
        for (int i = 1; i <= totalRooms; i++) {
            rooms.push_back(Room(i)); // Add rooms to the hotel
        }
    }

    // Function to book a room
    void bookRoom(string name) {
        for (auto &room : rooms) {
            if (!room.isBooked) { // Check if room is available
                room.isBooked = true; // Mark room as booked
                room.customerName = name; // Assign customer name
                cout << "Room " << room.roomNumber << " booked successfully for " << name << "!" << endl;
                return;
            }
        }
        cout << "Sorry, no rooms available!" << endl;
    }

    // Function to check room availability
    void checkAvailability() {
        bool available = false; // Flag to track available rooms
        for (auto &room : rooms) {
            if (!room.isBooked) { // If room is not booked
                cout << "Room " << room.roomNumber << " is available." << endl;
                available = true;
            }
        }
        if (!available)
            cout << "No rooms available." << endl;
    }

    // Function to display all bookings
    void displayBookings() {
        cout << "Current Bookings:" << endl;
        for (auto &room : rooms) {
            if (room.isBooked) { // Check if room is booked
                cout << "Room " << room.roomNumber << " is booked by " << room.customerName << "." << endl;
            }
        }
    }
};

// Main function to run the hotel booking system
int main() {
    Hotel myHotel(5); // Create a hotel with 5 rooms
    int choice; // Variable to store user choice
    string name; // Variable to store customer name

    do {
        // Display menu options
        cout << "\nHotel Booking System" << endl;
        cout << "1. Book a Room" << endl;
        cout << "2. Check Room Availability" << endl;
        cout << "3. Display Bookings" << endl;
        cout << "4. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice; // Take user input for choice

        switch (choice) {
        case 1:
            cout << "Enter your name: ";
            cin >> name; // Take customer name input
            myHotel.bookRoom(name); // Book a room
            break;
        case 2:
            myHotel.checkAvailability(); // Check room availability
            break;
        case 3:
            myHotel.displayBookings(); // Display booked rooms
            break;
        case 4:
            cout << "Exiting..." << endl; // Exit the system
            break;
        default:
            cout << "Invalid choice! Please try again." << endl; // Handle invalid input
        }
    } while (choice != 4); // Repeat until user exits

    return 0; // End of program
}

