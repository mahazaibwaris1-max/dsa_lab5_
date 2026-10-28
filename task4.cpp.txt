
#include <iostream>
#include <stack>
#include <string>
using namespace std;

class TextEditor {
private:
    string text;
    stack<string> undoStack;
    stack<string> redoStack;

public:
    void typeText(string value) {
        undoStack.push(text);
        text += value;

        while (!redoStack.empty()) {
            redoStack.pop();
        }

        cout << "Text added successfully.\n";
    }

    void deleteText() {
        if (text.empty()) {
            cout << "No text to delete.\n";
            return;
        }

        undoStack.push(text);
        text.pop_back();

        while (!redoStack.empty()) {
            redoStack.pop();
        }

        cout << "Last character deleted.\n";
    }

    void undo() {
        if (undoStack.empty()) {
            cout << "Nothing to undo.\n";
            return;
        }

        redoStack.push(text);
        text = undoStack.top();
        undoStack.pop();

        cout << "Undo successful.\n";
    }

    void redo() {
        if (redoStack.empty()) {
            cout << "Nothing to redo.\n";
            return;
        }

        undoStack.push(text);
        text = redoStack.top();
        redoStack.pop();

        cout << "Redo successful.\n";
    }

    void displayText() {
        cout << "Current text: " << text << endl;
    }
};

int main() {
    TextEditor editor;
    int choice;
    string value;

    do {
        cout << "\n===== TEXT EDITOR MENU =====\n";
        cout << "1. Type text\n";
        cout << "2. Delete last character\n";
        cout << "3. Undo\n";
        cout << "4. Redo\n";
        cout << "5. Display text\n";
        cout << "6. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            cout << "Enter text to add: ";
            getline(cin >> ws, value);
            editor.typeText(value);
            break;

        case 2:
            editor.deleteText();
            break;

        case 3:
            editor.undo();
            break;

        case 4:
            editor.redo();
            break;

        case 5:
            editor.displayText();
            break;

        case 6:
            cout << "Exiting text editor.\n";
            break;

        default:
            cout << "Invalid choice! Try again.\n";
        }

    } while (choice != 6);

    return 0;
}
