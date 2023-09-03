# Library Management System
## Librarian
### Attributes 

- books - static list of all books in the library
- members - static list of all members of the library
- latest_book_ID - an int that maintains the book ID to be assigned to the latest added book
- latest_member_ID - an int that maintains the member ID to be assigned to the latest added member

Design decision: When a book/member is removed, their bookID/memberID cannot be reassigned

### Methods

- addBook - every copy has a unique bookID
- removeBook - a book that is issued by someone or a book with an invalid bookID cannot be removed
- addMember - unique identifier of every member is the memberID, name and phone number can be repeated
- removeMember - a member with issued books or due fine cannot be removed
- listAllBooks - calls the toString() function of all the books in the static list 'books'
- listAvailableBooks - calls the toString() function of all the books in the static list 'books' which are currently not issued by anyone
- listAllMembers - calls the toString() function of all the members in the static list 'members'

## Member
### Attributes

- name
- phoneNumber
- age - redundant attribute
- memberID - unique identifier
- booksIssued - list of books issued currently
- fine - unpaid fine remaining after returning the books

### Methods

- listMyBooks - calls the toString() function of all the books in the list 'booksIssued'
- issueBook - a member cannot issue a book if they have due fine, 2 books already, the bookID is invalid, the book name and bookID don't match, or the book is issued by someone else already
- returnBook - a member cannot return a book they have not issued
- payFine - sets the fine to 0

Design Decision: Fine is calculated only when a book is returned. If the book is not returned but is overdue, it will neither reflect in the fine attribute of the member, nor will the librarian be able to see it. Extra fine is not charged for the time between returning the book and paying the fine.

## Book
### Attributes

- bookID - unique identifier 
- title 
- author
- status - false:book available, true: book issued
- issue_date - stores the timestamp of issuing

### Methods

- calculateFine - calculates fine when it is called (ie. when member returns the book) and the value is added to the fine attribute of the concerned member (to avoid overwriting an existing fine)

## Main

Interactive Menu

- implemented using nested if statements
- 'choice' is an int with limited range, uncanny values invite errors
- member has to enter all correct credentials to Enter as a member - increased safety