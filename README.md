# MS-SQL-Project
MS SQL Project by Kalpesh Parikh
SQL Project Title: Library Management System
Name – Kalpesh Parikh
Objective:
Build a basic database for a library system to manage books, members, and transactions like issuing and returning books.
Tasks:
1.	Create Tables:
○	Books: Contains details of all books in the library.
■	Columns: BookID, Title, Author, Genre, YearPublished, CopiesAvailable
○	Members: Contains details of library members.
■	Columns: MemberID, FirstName, LastName, DateOfBirth, MembershipDate
○	Transactions: Logs book issuance and returns.
■	Columns: TransactionID, MemberID, BookID, IssueDate, ReturnDate
Solution:
create table books(
book_id int Primary key,
title varchar(50),
author varchar(50),
genere varchar(50),
yearpublished year,
copiesavailable int
);
create table members(
member_id int Primary key,
firstname varchar(50),
lastname varchar(50),
dob date,
membershipdate date
);
create table transactions(
transaction_id int Primary key,
member_id int,
book_id int,
issuedate date,
returndate date,
FOREIGN KEY (book_id) REFERENCES books(book_id),
FOREIGN KEY (member_id) REFERENCES members(member_id)
);

2.	Insert Data:
Add sample data for books, members, and transactions.

Solution:

	Insert into Enterprise.books values(8, 'title8', 'author8', 'drama', 2004, 50);
Insert into Enterprise.members values(8, 'aplesh', 'mistry', '1975-08-02', '2002-08-30');
	Insert into Enterprise.transactions values(14, 2, 5, '2002-08-10', '2002-08-30');

3.	Queries to Practice:
○	Retrieve all books by a specific author.
Solution:
	SELECT * FROM enterprise.books
	where author = 'author2'

○	List books available in a particular genre.
Solution:
	SELECT * FROM enterprise.books
	where genere = 'drama'

○	Find members who joined in a specific year.
Solution:
	select * from enterprise.members
	where membershipdate = '2005-01-01'

○	Check which books are currently issued and their due dates.
Solution:
select * from enterprise.transactions
	where issuedate >= '2005-01-01'

○	Count the total number of books available in the library.
Solution:
	With new_transactions as 
	(SELECT book_id, count(book_id) as cbook_cnt 
    	 FROM enterprise.transactions 
	 group by book_id
    	 )
select b.book_id, (b.copiesavailable - nt.cbook_cnt)
from enterprise.books b
join new_transactions nt on b.book_id = nt.book_id;

4.	Advanced Queries (Optional):
○	Identify the member who has issued the most books.
Solution:
	SELECT member_id, count(book_id) as cnt
FROM enterprise.transactions
group by member_id
order by cnt desc

○	Generate a report of overdue books.
Solution:
	SELECT * 
FROM enterprise.transactions
where returndate is NULL

<img width="468" height="647" alt="image" src="https://github.com/user-attachments/assets/f7da59db-e96f-431e-90ab-c2bd6ed4de50" />
