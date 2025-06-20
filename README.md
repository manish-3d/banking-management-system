import random
import getpass

class BankAccount:
    def __init__(self, account_number, name, age, password, balance=0):
        self.account_number = account_number
        self.name = name
        self.age = age
        self.password = password
        self.balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            print(f"₹{amount} deposited successfully.")
        else:
            print("Deposit amount must be positive.")

    def withdraw(self, amount):
        if amount > 0:
            if self.balance >= amount:
                self.balance -= amount
                print(f"₹{amount} withdrawn successfully.")
            else:
                print("Insufficient balance.")
        else:
            print("Withdrawal amount must be positive.")

    def get_balance(self):
        return self.balance

    def display(self):
        print(f"Account Number: {self.account_number}")
        print(f"Name: {self.name}")
        print(f"Age: {self.age}")
        print(f"Balance: ₹{self.balance}")
        print("-" * 30)

def create_account(accounts):
    name = input("Enter your name: ")
    age = int(input("Enter your age: "))
    password = getpass.getpass("Set your password: ")
    balance = float(input("Enter initial deposit amount: "))
    account_number = random.randint(100000, 999999)

    account = BankAccount(account_number, name, age, password, balance)
    accounts.append(account)

    print("\nAccount created successfully!")
    print(f"Your account number is: {account_number}")
    print("-" * 30)

def enter_existing_account(accounts):
    try:
        acc_number = int(input("Enter your account number: "))
        password = getpass.getpass("Enter your password: ")
        for acc in accounts:
            if acc.account_number == acc_number and acc.password == password:
                print(f"Welcome {acc.name}!")
                return acc
        print("Invalid account number or password.")
    except ValueError:
        print("Invalid input. Please enter numbers only.")
    return None

def display_all_accounts(accounts):
    if not accounts:
        print("No accounts available.")
        return
    print("\nAll Accounts:")
    for acc in accounts:
        acc.display()

def delete_account(accounts, account):
    accounts.remove(account)
    print("Account deleted successfully.")

def main():
    accounts = []

    while True:
        print("\n=== Welcome to Simple Banking System ===")
        print("1. Create a New Account")
        print("2. Login to Existing Account")
        print("3. Display All Accounts")
        print("4. Exit")
        choice = input("Enter your choice: ")

        if choice == '1':
            create_account(accounts)

        elif choice == '2':
            account = enter_existing_account(accounts)
            if account:
                while True:
                    print("\n--- Account Menu ---")
                    print("1. Deposit")
                    print("2. Withdraw")
                    print("3. View Balance")
                    print("4. Delete Account")
                    print("5. Logout")
                    sub_choice = input("Enter your choice: ")

                    if sub_choice == '1':
                        amount = float(input("Enter deposit amount: "))
                        account.deposit(amount)

                    elif sub_choice == '2':
                        amount = float(input("Enter withdrawal amount: "))
                        account.withdraw(amount)

                    elif sub_choice == '3':
                        print(f"Current Balance: ₹{account.get_balance()}")

                    elif sub_choice == '4':
                        confirm = input("Are you sure you want to delete your account? (y/n): ").lower()
                        if confirm == 'y':
                            delete_account(accounts, account)
                            break

                    elif sub_choice == '5':
                        print("Logging out...")
                        break

                    else:
                        print("Invalid choice. Try again.")

        elif choice == '3':
            display_all_accounts(accounts)

        elif choice == '4':
            print("Thank you for using the banking system!")
            break

        else:
            print("Invalid choice. Please select from the menu.")

if __name__ == "__main__":
    main()
