CREATE DATABASE NumteryLibrary;

use NumteryLibrary;


CREATE TABLE Authors (
    author_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL
);

CREATE TABLE Books (
    book_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(255) NOT NULL,
    author_id INT NOT NULL,
    isbn VARCHAR(13) UNIQUE,
    publication_year INT,
    FOREIGN KEY (author_id) REFERENCES Authors(author_id)
);


CREATE TABLE Members (
    member_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    join_date DATE NOT NULL
);
CREATE TABLE BorrowedBooks (
    borrow_id INT PRIMARY KEY AUTO_INCREMENT,
    book_id INT NOT NULL,
    member_id INT NOT NULL,
    borrow_date DATE NOT NULL,
    return_date DATE,
    FOREIGN KEY (book_id) REFERENCES Books(book_id),
    FOREIGN KEY (member_id) REFERENCES Members(member_id)
);
INSERT INTO Books (title, author_id, isbn, publication_year)
VALUES ('To Kill a Mockingbird', 1, '9780061120084', 1960);
INSERT INTO BorrowedBooks (book_id, member_id, borrow_date, return_date)
VALUES (1, 1, CURDATE(), NULL);
UPDATE BorrowedBooks
SET return_date = CURDATE()
WHERE book_id = 1 AND member_id = 1 AND return_date IS NULL;
