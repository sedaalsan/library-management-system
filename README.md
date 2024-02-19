# library-management-system
class Library:
    def __init__(self, file1):
        self.file1 = file1
        try:
            self.file = open(self.file1, "a+")
        except FileNotFoundError:
            import os
            os.makedirs(os.path.dirname(self.file1), exist_ok=True)
            self.file = open(self.file1, "a+")

    def __del__(self):
        self.file.close()
while True:
    print("*** MENU ***")
    print("1) List Books")
    print("2) Add Book")
    print("3) Remove Book")
    print("q) Quit")

    choice = input("Enter your choice: ")
    if choice == "1":
        lib.list_books()
    elif choice == "2":
        lib.add_book()
    elif choice == "3":
        lib.remove_book()
    elif choice.lower() == "q":
        break
    else:
        print("Invalid choice!")
    def list_books(self):
            self.file.seek(0)  
            lines = self.file.read().splitlines()  
            for line in lines:
                book_info = line.split(",")
                book_name = book_info[0]
                author = book_info[1]
                print(f"{book_name}, {author}")

    def add_book(self):
            book_title = input("Enter book title: ")
            book_author = input("Enter book author: ")
            release_year = input("Enter release year: ")
            number_pages = input("Enter number of pages: ")

            book_info = f"{book_title},{book_author},{release_year},{number_pages}\n"
            self.file.write(book_info)
            print("Book has been added successfully!")

    def remove_book(self):
            title_to_remove = input("Enter the title of the book to remove: ")
            self.file.seek(0)  
            lines = self.file.readlines()  

            updated_lines = [line for line in lines if not line.startswith(title_to_remove)]

            self.file.seek(0)
            self.file.truncate()

            self.file.writelines(updated_lines)
            print("Book has been removed successfully!")


lib = Library("books.txt")
