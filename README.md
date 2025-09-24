import os
os.chdir("/tmp")   # Linux temporary folder, always writable
menu = {
    1: "Create File",
    2: "Insert Content",
    3: "Replace Content",
    4: "Append Content",
    5: "Read File",
    6: "Rename File",
    7: "Delete File",
    8: "Show Working Directory",
    9: "Change Directory",
    10: "Exit"
}

def create_file(filename):
    with open(filename, "w") as f:
        pass  # just create empty file
    print(f"File '{filename}' created successfully.")

def insert_content(filename, content):
    with open(filename, "w") as f:
        f.write(content)
    print("Content inserted (old content removed).")

def replace_content(filename, old, new):
    try:
        with open(filename, "r") as f:
            data = f.read()
        data = data.replace(old, new)
        with open(filename, "w") as f:
            f.write(data)
        print("Content replaced successfully.")
    except FileNotFoundError:
        print("File not found.")

def append_content(filename, content):
    try:
        with open(filename, "a") as f:
            f.write(content)
        print("Content appended successfully.")
    except FileNotFoundError:
        print("File not found.")

def read_file(filename):
    try:
        with open(filename, "r") as f:
            print("\nFile Content:\n", f.read())
    except FileNotFoundError:
        print("File not found.")

def rename_file(old, new):
    try:
        os.rename(old, new)
        print(f"Renamed '{old}' to '{new}'.")
    except FileNotFoundError:
        print("File not found.")

def delete_file(filename):
    try:
        os.remove(filename)
        print(f"File '{filename}' deleted.")
    except FileNotFoundError:
        print("File not found.")

def show_working_dir():
    print("Current Working Directory:", os.getcwd())

def change_dir(path):
    try:
        os.chdir(path)
        print("Directory changed to:", os.getcwd())
    except FileNotFoundError:
        print("Directory not found.")


files_list = []                
file_types = ("txt", "log")  
unique_files = set()          
def main():
    while True:
        
        print("\nAvailable Operations:")
        for key, value in menu.items():
            print(f"{key}. {value}")

        try:
            choice = int(input("\nEnter your choice: "))
        except ValueError:
            print("Invalid input. Try again.")
            continue

        if choice == 1:
            filename = input("Enter filename: ")
            create_file(filename)
            files_list.append(filename)
            unique_files.add(filename)

        elif choice == 2:
            filename = input("Enter filename: ")
            content = input("Enter content: ")
            insert_content(filename, content)

        elif choice == 3:
            filename = input("Enter filename: ")
            old = input("Enter word to replace: ")
            new = input("Enter new word: ")
            replace_content(filename, old, new)

        elif choice == 4:
            filename = input("Enter filename: ")
            content = input("Enter content to append: ")
            append_content(filename, content)

        elif choice == 5:
            filename = input("Enter filename: ")
            read_file(filename)

        elif choice == 6:
            old = input("Enter old filename: ")
            new = input("Enter new filename: ")
            rename_file(old, new)

        elif choice == 7:
            filename = input("Enter filename to delete: ")
            delete_file(filename)
            if filename in files_list:
                files_list.remove(filename)
                unique_files.discard(filename)

        elif choice == 8:
            show_working_dir()

        elif choice == 9:
            path = input("Enter directory path: ")
            change_dir(path)

        elif choice == 10:
            print("Exiting program...")
            break   

        else:
            print("Invalid choice. Try again.")

    
        if not files_list:
            pass  

# Run program
if __name__ == "__main__":
    main()
