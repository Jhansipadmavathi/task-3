import json

def load_contacts():
    try:
        with open("contacts.json", "r") as file:
            return json.load(file)
    except FileNotFoundError:
        return {}

def save_contacts(contacts):
    with open("contacts.json", "w") as file:
        json.dump(contacts, file, indent=4)

def add_contact(contacts):
    name = input("Enter name: ")
    phone = input("Enter phone number: ")
    email = input("Enter email: ")
    address = input("Enter address: ")

    contacts[name] = {"phone": phone, "email": email, "address": address}
    print("Contact added successfully.")

def view_contacts(contacts):
    if contacts:
        print("Contact List:")
        for name, details in contacts.items():
            print(f"Name: {name}, Phone: {details['phone']}")
    else:
        print("No contacts found.")

def search_contact(contacts):
    search_term = input("Enter name or phone number to search: ")
    found_contacts = {name: details for name, details in contacts.items()
                      if search_term.lower() in name.lower() or search_term in details["phone"]}
    
    if found_contacts:
        print("Search Results:")
        for name, details in found_contacts.items():
            print(f"Name: {name}, Phone: {details['phone']}, Email: {details['email']}, Address: {details['address']}")
    else:
        print("No contacts found.")

def update_contact(contacts):
    name = input("Enter the name of the contact to update: ")
    
    if name in contacts:
        print("Enter new details (leave blank to keep current value):")
        phone = input(f"New phone number (current: {contacts[name]['phone']}): ")
        email = input(f"New email (current: {contacts[name]['email']}): ")
        address = input(f"New address (current: {contacts[name]['address']}): ")

        if phone:
            contacts[name]["phone"] = phone
        if email:
            contacts[name]["email"] = email
        if address:
            contacts[name]["address"] = address
        
        print("Contact updated successfully.")
    else:
        print("Contact not found.")

def delete_contact(contacts):
    name = input("Enter the name of the contact to delete: ")

    if name in contacts:
        del contacts[name]
        print("Contact deleted successfully.")
    else:
        print("Contact not found.")

def main():
    contacts = load_contacts()

    while True:
        print("\nContact Management System")
        print("1. Add Contact")
        print("2. View Contacts")
        print("3. Search Contact")
        print("4. Update Contact")
        print("5. Delete Contact")
        print("6. Exit")

        choice = input("Enter your choice: ")

        if choice == '1':
            add_contact(contacts)
        elif choice == '2':
            view_contacts(contacts)
        elif choice == '3':
            search_contact(contacts)
        elif choice == '4':
            update_contact(contacts)
        elif choice == '5':
            delete_contact(contacts)
        elif choice == '6':
            save_contacts(contacts)
            print("Exiting the program. Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

if _name_ == "_main_":
    main()
