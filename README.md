# Codsoft-Task-5
import json

# Define a function to load contacts from a file
def load_contacts(filename='contacts.json'):
    try:
        with open(filename, 'r') as file:
            return json.load(file)
    except (FileNotFoundError, json.JSONDecodeError):
        return {}

# Define a function to save contacts to a file
def save_contacts(contacts, filename='contacts.json'):
    with open(filename, 'w') as file:
        json.dump(contacts, file, indent=4)

# Function to add a contact
def add_contact(contacts):
    name = input("Enter name: ")
    phone = input("Enter phone number: ")
    email = input("Enter email address: ")

    # Add contact to the dictionary
    contacts[name] = {
        'phone': phone,
        'email': email
    }
    print(f"Contact for {name} added successfully!")

# Function to display all contacts
def display_contacts(contacts):
    if not contacts:
        print("No contacts in the contact book.")
    else:
        for name, info in contacts.items():
            print(f"Name: {name}")
            print(f"Phone: {info['phone']}")
            print(f"Email: {info['email']}")
            print("-" * 20)

# Function to search for a contact
def search_contact(contacts):
    name = input("Enter the name to search: ")
    if name in contacts:
        info = contacts[name]
        print(f"Name: {name}")
        print(f"Phone: {info['phone']}")
        print(f"Email: {info['email']}")
    else:
        print(f"No contact found for {name}.")

# Function to update a contact's details
def update_contact(contacts):
    name = input("Enter the name of the contact to update: ")
    if name in contacts:
        print(f"Current details: {contacts[name]}")
        phone = input(f"Enter new phone number for {name} (leave empty to keep current): ")
        email = input(f"Enter new email address for {name} (leave empty to keep current): ")

        # Update if the user has provided new data
        if phone:
            contacts[name]['phone'] = phone
        if email:
            contacts[name]['email'] = email

        print(f"Contact for {name} updated successfully!")
    else:
        print(f"No contact found for {name}.")

# Function to delete a contact
def delete_contact(contacts):
    name = input("Enter the name of the contact to delete: ")
    if name in contacts:
        del contacts[name]
        print(f"Contact for {name} deleted successfully!")
    else:
        print(f"No contact found for {name}.")

# Main function
def show_menu():
    print("\n--- Contact Book ---")
    print("1. Add Contact")
    print("2. View All Contacts")
    print("3. Search for Contact")
    print("4. Update Contact")
    print("5. Delete Contact")
    print("6. Exit")

def main():
    contacts = load_contacts()

    while True:
        show_menu()
        choice = input("Enter your choice (1-6): ")

        if choice == '1':
            add_contact(contacts)
        elif choice == '2':
            display_contacts(contacts)
        elif choice == '3':
            search_contact(contacts)
        elif choice == '4':
            update_contact(contacts)
        elif choice == '5':
            delete_contact(contacts)
        elif choice == '6':
            save_contacts(contacts)
            print("Exiting... All changes saved.")
            break
        else:
            print("Invalid choice. Please choose a number between 1 and 6.")

if __name__ == "__main__":
    main()
