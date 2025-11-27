#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int value) {
        data = value;
        left = right = nullptr;
    }
};

Node* insert(Node* root, int value) {
    if (root == nullptr)
        return new Node(value);

    if (value < root->data)
        root->left = insert(root->left, value);
    else if (value > root->data)
        root->right = insert(root->right, value);

    return root;
}



bool search(Node* root, int value) {
    if (root == nullptr)
        return false;

    if (root->data == value)
        return true;
    else if (value < root->data)
        return search(root->left, value);
    else
        return search(root->right, value);
}



void displayAscending(Node* root) {
    if (root == nullptr)
        return;

    displayAscending(root->left);
    cout << root->data << " ";
    displayAscending(root->right);
}


int main() {
    Node* root = nullptr;
    int choice, bookID;

    do {
        cout << "\n\n--- Smart Library System ---\n";
        cout << "1. Add returned Book ID\n";
        cout << "2. Check if a Book ID was returned\n";
        cout << "3. Display all returned Book IDs in ascending order\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            cout << "Enter Book ID to add: ";
            cin >> bookID;
            root = insert(root, bookID);
            cout << "Book ID stored successfully.\n";
            break;

        case 2:
            cout << "Enter Book ID to search: ";
            cin >> bookID;
            if (search(root, bookID))
                cout << "Book ID WAS returned.\n";
            else
                cout << "Book ID NOT returned yet.\n";
            break;

        case 3:
            cout << "Books returned today (sorted): ";
            displayAscending(root);
            cout << "\n";
            break;

        case 4:
            cout << "Exiting system...\n";
            break;

        default:
            cout << "Invalid choice! Try again.\n";
        }

    } while (choice != 4);

    return 0;
}
