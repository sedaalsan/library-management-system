# library-management-system
class Library:
    def __init__(self):
        self.file = open("books.txt", "a+") #read and append
        self.file.close()
        self.file = open("books.txt", "r+") #read and write
        
#Close the file when the 'Library' object is destroyed.
    def __del__(self):
        self.file.close()

    def list_books(self):
        self.file.seek(0)
        books = self.file.readlines()
        if not books:
            print("No books available.")
        else:
            print("List of books:")
            for book in books:
                book_info = book.strip().split(',')
                print(f"Title: {book_info[0]}, Author: {book_info[1]}")

    def add_book(self):
        title = input("Enter book title: ")
        author = input("Enter book author: ")
        release_year = input("Enter release year: ")
        num_pages = input("Enter number of pages: ")
        book_info = f"{title},{author},{release_year},{num_pages}\n"
        self.file.write(book_info)
        print("Book added successfully.")

    def remove_book(self):
        title = input("Enter the title of the book to remove: ")
        self.file.seek(0)
        books = self.file.readlines()
        new_books = []
        removed = False
        for book in books:
            if title in book:
                removed = True
            else:
                new_books.append(book)
        if not removed:
            print("Book not found.")
        else:
            self.file.seek(0)
            self.file.truncate()
            self.file.writelines(new_books)
            print("Book removed successfully.")

lib = Library()

while True:
    print("*** MENU***")
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
        print("Invalid choice. Please try again.")

