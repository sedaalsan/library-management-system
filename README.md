# library-management-system
file1 = open("books.txt","a+",encoding="utf-8")
read1 = file1.read()
print(read1)

class Library:
    bookslist = {}
    def __init__(self):
        while True:
            print("***MENU***")
            print("""
        1)List Books
        2)Add Book
        3)Remove Book
        q)Quit""")
            choice=int(input("Enter your choice (1-4): "))
            if (choice==1):
                self.listbook()
            elif (choice==2):
                self.bookadd()
            elif (choice==3):
                self.removebook()
            #elif (choice == q):
                #choice=str(choice)
                #self.cikis()
            else:
                print("Invalid input. Please try again.")
                continue
    def bookadd(self):
        self.bookname=input("Enter the book title: ")
        self.bookauthor=input("Enter the author: ")
        self.bookyear=input("Enter the release year: ")
        self.bookpage=input("Enter the number of pages: ")
        self.bookslist[self.bookname]={
            "bookname":self.bookname,
            "bookauthor":self.bookauthor,
            "bookyear":self.bookyear,
            "bookpage":self.bookpage,
        }
        print("Information was recorded.")

    def listbook(self):
        if(self.bookslist=={}):
            print("The book information not found")
        else:
            for book in self.bookslist:
                print(book,self.bookslist[book])
    def removebook(self):
        book_name = input("Enter the book name: ")
        books = self.file.readlines()
        new_books = []
        removed = False
        for book in books:
            bookslist = book.split(",")
            if book_name == bookslist[0]:
                removed = True
            else:
                new_books.append(book)
            if not removed:
              self.file.seek(0)
              self.file.truncate()
              self.file.close()
              file2 = open("temp.txt", "a", encoding="utf-8")
              for book in new_books:
                file2.write(book)
                print(f"{book_name} removed")

            else:
                print(f"{book_name} not found.") 
        #def cikis(self):
            #print("Program has been closed.")
            #exit(0)
lib=Library()
