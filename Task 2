#include <iostream>
#include <fstream>
#include <cstring>
using namespace std;

#define MAX_NAME_LENGTH 100
#define MAX_DISEASE_LENGTH 100
#define FILE_NAME "patient_records.dat"

struct Patient {
    int patientID;
    char name[MAX_NAME_LENGTH];
    int age;
    char disease[MAX_DISEASE_LENGTH];
    int roomNumber;
};

// Function declarations
void addPatient();
void searchPatientByID();
void displayAllPatients();
void loadPatientRecords();
void savePatientRecords();
int getNextPatientID();

// Global variables
Patient patients[100];
int patientCount = 0;

int main() {
    int choice;

    // Load patient records from file at the program start
    loadPatientRecords();

    while (true) {
        cout << "\nHospital Management System\n";
        cout << "1. Add New Patient\n";
        cout << "2. Search for a Patient by Patient ID\n";
        cout << "3. Display All Patients\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;
        cin.ignore();  // Clear the buffer after reading an integer

        switch (choice) {
            case 1:
                addPatient();
                break;
            case 2:
                searchPatientByID();
                break;
            case 3:
                displayAllPatients();
                break;
            case 4:
                savePatientRecords();
                cout << "Exiting the system. Goodbye!\n";
                return 0;
            default:
                cout << "Invalid choice, please try again.\n";
        }
    }

    return 0;
}

// Function to add a new patient to the records
void addPatient() {
    Patient newPatient;

    newPatient.patientID = getNextPatientID();
    cin.ignore();  // Clear buffer

    cout << "Enter patient name: ";
    cin.getline(newPatient.name, MAX_NAME_LENGTH);

    cout << "Enter patient age: ";
    cin >> newPatient.age;
    cin.ignore();  // Clear the buffer after reading an integer

    cout << "Enter patient's disease: ";
    cin.getline(newPatient.disease, MAX_DISEASE_LENGTH);

    cout << "Enter room number: ";
    cin >> newPatient.roomNumber;
    cin.ignore();  // Clear the buffer

    patients[patientCount] = newPatient;
    patientCount++;

    cout << "Patient added successfully with Patient ID: " << newPatient.patientID << endl;
}

// Function to search for a patient by Patient ID
void searchPatientByID() {
    int searchID;
    bool found = false;

    cout << "Enter Patient ID to search: ";
    cin >> searchID;
    cin.ignore();  // Clear the buffer

    for (int i = 0; i < patientCount; i++) {
        if (patients[i].patientID == searchID) {
            cout << "\nPatient Found:\n";
            cout << "Patient ID: " << patients[i].patientID << endl;
            cout << "Name: " << patients[i].name << endl;
            cout << "Age: " << patients[i].age << endl;
            cout << "Disease: " << patients[i].disease << endl;
            cout << "Room Number: " << patients[i].roomNumber << endl;
            found = true;
            break;
        }
    }

    if (!found) {
        cout << "Patient not found.\n";
    }
}

// Function to display all the admitted patients
void displayAllPatients() {
    if (patientCount == 0) {
        cout << "No patients admitted.\n";
    } else {
        cout << "\nAll Patients in Hospital:\n";
        for (int i = 0; i < patientCount; i++) {
            cout << "\nPatient ID: " << patients[i].patientID << endl;
            cout << "Name: " << patients[i].name << endl;
            cout << "Age: " << patients[i].age << endl;
            cout << "Disease: " << patients[i].disease << endl;
            cout << "Room Number: " << patients[i].roomNumber << endl;
        }
    }
}

// Function to get the next available Patient ID (incremental)
int getNextPatientID() {
    return patientCount + 1;
}

// Function to load the patient records from a file
void loadPatientRecords() {
    ifstream file(FILE_NAME, ios::binary);
    if (file.is_open()) {
        file.read((char*)&patientCount, sizeof(patientCount));
        file.read((char*)patients, sizeof(Patient) * patientCount);
        file.close();
    }
}

// Function to save the patient records to a file
void savePatientRecords() {
    ofstream file(FILE_NAME, ios::binary);
    if (file.is_open()) {
        file.write((char*)&patientCount, sizeof(patientCount));
        file.write((char*)patients, sizeof(Patient) * patientCount);
        file.close();
    }
}
