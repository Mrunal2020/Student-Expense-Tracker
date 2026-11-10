import csv
import os

filename = "expenses.csv"

def add_expense():
    date = input("Enter date (DD-MM-YYYY): ")
    category = input("Enter category (Food/Travel/Shopping/Other): ")
    amount = float(input("Enter amount: "))
    description = input("Enter description: ")

    file_exists = os.path.exists(filename)

    with open(filename, "a", newline="") as file:
        writer = csv.writer(file)

        if not file_exists:
            writer.writerow(["Date", "Category", "Amount", "Description"])

        writer.writerow([date, category, amount, description])

    print("Expense added successfully!")

def view_expenses():
    if not os.path.exists(filename):
        print("No expenses recorded yet.")
        return

    with open(filename, "r") as file:
        reader = csv.reader(file)

        for row in reader:
            print(row)

def total_expenses():
    total = 0

    if not os.path.exists(filename):
        print("No expenses recorded yet.")
        return

    with open(filename, "r") as file:
        reader = csv.reader(file)
        next(reader, None)

        for row in reader:
            total += float(row[2])

    print("Total expenses: Rs.", total)

while True:
    print("\n===== STUDENT EXPENSE TRACKER =====")
    print("1. Add Expense")
    print("2. View Expenses")
    print("3. Calculate Total Expenses")
    print("4. Exit")

    choice = input("Enter your choice: ")

    if choice == "1":
        add_expense()
    elif choice == "2":
        view_expenses()
    elif choice == "3":
        total_expenses()
    elif choice == "4":
        print("Thank you for using Student Expense Tracker!")
        break
    else:
        print("Invalid choice. Try again.")