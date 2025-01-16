#include <iostream>
#include <fstream>
#include <cstring>
using namespace std;

#define MAX_TITLE_LENGTH 100
#define MAX_AUTHOR_LENGTH 100
#define FILE_NAME "library_inventory.dat"

struct Book {
    int bookID;
    char title[MAX_TITLE_LENGTH];
    char author[MAX_AUTHOR_LENGTH];
    int quantity;
};

// Function declarations
void addBook();
void searchBook();
void displayBooks();
void loadInventory();
void saveInventory();
int getNextBookID();

// Global variables
Book inventory[100];
int bookCount = 0;

int main() {
    int choice;

    // Load inventory from file at program start
    loadInventory();

    while (true) {
        cout << "\nLibrary Management System\n";
        cout << "1. Add New Book\n";
        cout << "2. Search for a Book\n";
        cout << "3. Display All Books\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;
        cin.ignore();  // Clear the buffer after reading an integer

        switch (choice) {
            case 1:
                addBook();
                break;
            case 2:
                searchBook();
                break;
            case 3:
                displayBooks();
                break;
            case 4:
                saveInventory();
                cout << "Exiting the system. Goodbye!\n";
                return 0;
            default:
                cout << "Invalid choice, please try again.\n";
        }
    }

    return 0;
}

// Function to add a new book to the inventory
void addBook() {
    Book newBook;

    newBook.bookID = getNextBookID();
    cin.ignore();  // Clear buffer

    cout << "Enter book title: ";
    cin.getline(newBook.title, MAX_TITLE_LENGTH);

    cout << "Enter author name: ";
    cin.getline(newBook.author, MAX_AUTHOR_LENGTH);

    cout << "Enter book quantity: ";
    cin >> newBook.quantity;
    cin.ignore();  // Clear the buffer after reading an integer

    inventory[bookCount] = newBook;
    bookCount++;

    cout << "Book added successfully with Book ID: " << newBook.bookID << endl;
}

// Function to search for a book by ID or title
void searchBook() {
    int choice;
    char searchTitle[MAX_TITLE_LENGTH];
    int searchID;
    bool found = false;

    cout << "Search by:\n";
    cout << "1. Book ID\n";
    cout << "2. Title\n";
    cout << "Enter your choice: ";
    cin >> choice;
    cin.ignore();  // Clear the buffer after reading an integer

    if (choice == 1) {
        cout << "Enter Book ID: ";
        cin >> searchID;
        cin.ignore();  // Clear the buffer

        for (int i = 0; i < bookCount; i++) {
            if (inventory[i].bookID == searchID) {
                cout << "\nBook found:\n";
                cout << "Book ID: " << inventory[i].bookID << endl;
                cout << "Title: " << inventory[i].title << endl;
                cout << "Author: " << inventory[i].author << endl;
                cout << "Quantity: " << inventory[i].quantity << endl;
                found = true;
                break;
            }
        }
    } else if (choice == 2) {
        cout << "Enter Book Title: ";
        cin.getline(searchTitle, MAX_TITLE_LENGTH);

        for (int i = 0; i < bookCount; i++) {
            if (strcmp(inventory[i].title, searchTitle) == 0) {
                cout << "\nBook found:\n";
                cout << "Book ID: " << inventory[i].bookID << endl;
                cout << "Title: " << inventory[i].title << endl;
                cout << "Author: " << inventory[i].author << endl;
                cout << "Quantity: " << inventory[i].quantity << endl;
                found = true;
                break;
            }
        }
    }

    if (!found) {
        cout << "Book not found.\n";
    }
}

// Function to display all books in the inventory
void displayBooks() {
    if (bookCount == 0) {
        cout << "No books available in the inventory.\n";
    } else {
        cout << "\nAll Books in Inventory:\n";
        for (int i = 0; i < bookCount; i++) {
            cout << "\nBook ID: " << inventory[i].bookID << endl;
            cout << "Title: " << inventory[i].title << endl;
            cout << "Author: " << inventory[i].author << endl;
            cout << "Quantity: " << inventory[i].quantity << endl;
        }
    }
}

// Function to get the next available book ID (incremental)
int getNextBookID() {
    return bookCount + 1;
}

// Function to load the book inventory from a file
void loadInventory() {
    ifstream file(FILE_NAME, ios::binary);
    if (file.is_open()) {
        file.read((char*)&bookCount, sizeof(bookCount));
        file.read((char*)inventory, sizeof(Book) * bookCount);
        file.close();
    }
}

// Function to save the book inventory to a file
void saveInventory() {
    ofstream file(FILE_NAME, ios::binary);
    if (file.is_open()) {
        file.write((char*)&bookCount, sizeof(bookCount));
        file.write((char*)inventory, sizeof(Book) * bookCount);
        file.close();
    }
}
