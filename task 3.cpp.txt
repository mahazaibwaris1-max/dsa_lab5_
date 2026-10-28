
#include <iostream>
#include <string>
using namespace std;

class myCarStack {
private:
    string cars[8];
    int carTop;

public:
    myCarStack() {
        carTop = -1;
    }

    bool isEmpty() const {
        return carTop == -1;
    }

    bool isFull() const {
        return carTop == 7;
    }

    int count() const {
        return carTop + 1;
    }

    void push(string car) {
        if (isFull()) {
            cout << "Parking lot is full!\n";
            return;
        }

        cars[++carTop] = car;
        cout << "Car " << car << " parked successfully.\n";
    }

    string pop() {
        if (isEmpty()) {
            return "";
        }

        return cars[carTop--];
    }

    string top() const {
        if (isEmpty()) {
            return "";
        }

        return cars[carTop];
    }

    bool search(string car) const {
        for (int i = 0; i <= carTop; i++) {
            if (cars[i] == car) {
                return true;
            }
        }
        return false;
    }

    void display() const {
        if (isEmpty()) {
            cout << "No cars are parked.\n";
            return;
        }

        cout << "Cars in parking lot (top to bottom):\n";
        for (int i = carTop; i >= 0; i--) {
            cout << cars[i] << endl;
        }
    }

    void removeCar(string car) {
        if (!search(car)) {
            cout << "Car " << car << " not found.\n";
            return;
        }

        myCarStack temp;

        while (top() != car) {
            temp.push(pop());
        }

        pop();
        cout << "Car " << car << " removed successfully.\n";

        while (!temp.isEmpty()) {
            push(temp.pop());
        }
    }
};

int main() {
    myCarStack parking;
    int choice;
    string car;

    do {
        cout << "\n===== PARKING LOT MENU =====\n";
        cout << "1. Park a new car\n";
        cout << "2. Remove a car\n";
        cout << "3. View parked cars\n";
        cout << "4. Show total cars parked\n";
        cout << "5. Show top car\n";
        cout << "6. Search for a car\n";
        cout << "7. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            if (parking.isFull()) {
                cout << "Parking lot is full!\n";
            }
            else {
                cout << "Enter car number: ";
                cin >> car;

                if (parking.search(car)) {
                    cout << "This car is already parked.\n";
                }
                else {
                    parking.push(car);
                }
            }
            break;

        case 2:
            cout << "Enter car number to remove: ";
            cin >> car;
            parking.removeCar(car);
            break;

        case 3:
            parking.display();
            break;

        case 4:
            cout << "Total cars parked: "
                << parking.count() << "/8\n";
            break;

        case 5:
            if (parking.isEmpty()) {
                cout << "No cars are parked.\n";
            }
            else {
                cout << "Top car: " << parking.top() << endl;
            }
            break;

        case 6:
            cout << "Enter car number to search: ";
            cin >> car;

            if (parking.search(car)) {
                cout << "Car " << car << " is present in the parking lot.\n";
            }
            else {
                cout << "Car " << car << " is not present.\n";
            }
            break;

        case 7:
            cout << "Exiting program.\n";
            break;

        default:
            cout << "Invalid choice! Try again.\n";
        }

    } while (choice != 7);

    return 0;
}
