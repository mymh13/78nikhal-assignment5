## Code example for assignment 1 b
  
```sql
SELECT 
    m.Movie_title, 
    CONCAT(a.Actor_firstname, ' ', a.Actor_lastname) AS ActorName,
    (SELECT AVG(r.Rating_value) 
     FROM rating r 
     WHERE r.Movie_ID = m.Movie_ID) AS AvgRating
FROM 
    movie m
JOIN 
    movieactor ma ON m.Movie_ID = ma.Movie_ID
JOIN 
    actor a ON ma.Actor_ID = a.Actor_ID
WHERE 
    m.Movie_ID IN (SELECT Movie_ID FROM ticket WHERE Ticket_price > 100);
```
  
### Pseudocode for above example for assignment 1 b  
  
```sql
VÄLJ 
    m.Movie_title, 
    SLÅIHOP(a.Actor_firstname, ' ', a.Actor_lastname) SOM ActorName,
    (VÄLJ GENOMSNITT(r.Rating_value) 
     FRÅN rating r 
     DÄR r.Movie_ID = m.Movie_ID) SOM AvgRating
FRÅN 
    movie m
FÖRENA 
    movieactor ma PÅ m.Movie_ID = ma.Movie_ID
FÖRENA 
    actor a PÅ ma.Actor_ID = a.Actor_ID
DÄR 
    m.Movie_ID FINNSI (VÄLJ Movie_ID FRÅN ticket DÄR Ticket_price > 100);
```
  
## Code example for above example for assignment 2 a - case 1  
  
```sql
  CREATE VIEW HighSpendingCustomers AS
SELECT 
    c.Customer_ID, 
    c.Customer_firstname, 
    c.Customer_lastname, 
    AVG(t.Ticket_price) AS AvgMonthlySpending
FROM 
    customer c
JOIN 
    customerticket ct ON c.Customer_ID = ct.Customer_ID
JOIN 
    ticket t ON ct.Ticket_ID = t.Ticket_ID
WHERE 
    YEAR(t.Ticket_purchasedate) = YEAR(CURDATE()) 
GROUP BY 
    c.Customer_ID, c.Customer_firstname, c.Customer_lastname
HAVING 
    AVG(t.Ticket_price) > 500;
```
  
## Code example for above example for assignment 2 a - case 2  
  
```sql
UPDATE customer
SET discount = 0.10
WHERE Customer_ID IN (
    SELECT Customer_ID FROM HighSpendingCustomers
);
```