# Student-Management-System
Python-based Student Management System using File Handling
import os

FILE_NAME = "students.txt"


def add_student():
    roll_no = input("Enter Roll Number: ")
    name = input("Enter Student Name: ")
    department = input("Enter Department: ")

    with open(FILE_NAME, "a") as file:
        file.write(f"{roll_no},{name},{department}\n")

    print("✅ Student Added Successfully!")


def view_students():
    if not os.path.exists(FILE_NAME):
        print("❌ No records found.")
        return

    with open(FILE_NAME, "r") as file:
        records = file.readlines()

    if len(records) == 0:
        print("❌ No students available.")
        return

    print("\n--- Student Records ---")
    for record in records:
        roll_no, name, department = record.strip().split(",")
        print(f"Roll No: {roll_no}")
        print(f"Name: {name}")
        print(f"Department: {department}")
        print("-" * 30)


def search_student():
    roll_search = input("Enter Roll Number to Search: ")

    if not os.path.exists(FILE_NAME):
        print("❌ No records found.")
        return

    found = False

    with open(FILE_NAME, "r") as file:
        for record in file:
            roll_no, name, department = record.strip().split(",")

            if roll_no == roll_search:
                print("\n✅ Student Found")
                print(f"Roll No: {roll_no}")
                print(f"Name: {name}")
                print(f"Department: {department}")
                found = True
                break

    if not found:
        print("❌ Student Not Found")


def delete_student():
    roll_delete = input("Enter Roll Number to Delete: ")

    if not os.path.exists(FILE_NAME):
        print("❌ No records found.")
        return

    records = []
    deleted = False

    with open(FILE_NAME, "r") as file:
        for record in file:
            roll_no, name, department = record.strip().split(",")

            if roll_no != roll_delete:
                records.append(record)
            else:
                deleted = True

    with open(FILE_NAME, "w") as file:
        file.writelines(records)

    if deleted:
        print("✅ Student Deleted Successfully")
    else:
        print("❌ Student Not Found")


def main():
    while True:
        print("\n===== STUDENT MANAGEMENT SYSTEM =====")
        print("1. Add Student")
        print("2. View Students")
        print("3. Search Student")
        print("4. Delete Student")
        print("5. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            add_student()

        elif choice == "2":
            view_students()

        elif choice == "3":
            search_student()

        elif choice == "4":
            delete_student()

        elif choice == "5":
            print("👋 Thank you!")
            break

        else:
            print("❌ Invalid Choice")


if __name__ == "__main__":
    main()
