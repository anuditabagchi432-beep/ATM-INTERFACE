# ATM-INTERFACE

ATM INTERFACE IN C++

#include <iostream>
#include <string>
#include <limits>

class ATM {
private:
    double balance;
    int pin;

public:
    ATM(double initialBalance, int initialPin) : balance(initialBalance), pin(initialPin) {}

    bool authenticate(int inputPin) {
        return inputPin == pin;
    }

    void checkBalance() {
        std::cout << "\nCurrent Balance: $" << balance << std::endl;
    }

    void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            std::cout << "Successfully deposited $" << amount << std::endl;
        } else {
            std::cout << "Invalid deposit amount." << std::endl;
        }
    }

    void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            std::cout << "Successfully withdrew $" << amount << std::endl;
        } else if (amount > balance) {
            std::cout << "Insufficient funds!" << std::endl;
        } else {
            std::cout << "Invalid withdrawal amount." << std::endl;
        }
    }
};

int main() {
    ATM myATM(1000.0, 1234); // Starting balance $1000, PIN 1234
    int inputPin, choice;
    double amount;

    std::cout << "Enter PIN to access ATM: ";
    std::cin >> inputPin;

    if (!myATM.authenticate(inputPin)) {
        std::cout << "Invalid PIN. Access Denied." << std::endl;
        return 0;
    }

    do {
        std::cout << "\n--- ATM Menu ---" << std::endl;
        std::cout << "1. Check Balance\n2. Deposit\n3. Withdraw\n4. Exit\nChoice: ";
        std::cin >> choice;

        switch (choice) {
            case 1: myATM.checkBalance(); break;
            case 2:
                std::cout << "Enter amount to deposit: ";
                std::cin >> amount;
                myATM.deposit(amount);
                break;
            case 3:
                std::cout << "Enter amount to withdraw: ";
                std::cin >> amount;
                myATM.withdraw(amount);
                break;
            case 4: std::cout << "Thank you for using our ATM." << std::endl; break;
            default: std::cout << "Invalid choice." << std::endl;
        }
    } while (choice != 4);

    return 0;
}
