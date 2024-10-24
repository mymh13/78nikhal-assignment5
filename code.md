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
  
## Code example for above example for assignment 2 b - admin table 
  
```sql
CREATE TABLE admin (
    Admin_ID INT PRIMARY KEY AUTO_INCREMENT,
    Admin_username VARCHAR(15),
    Admin_email VARCHAR(50),
    Admin_password VARCHAR(255),
    IsSuperAdmin BOOLEAN DEFAULT FALSE
);
```
  
## Code example for above example for assignment 2 b - personal info
  
```sql
CREATE TABLE personal_info (
    Person_ID INT PRIMARY KEY AUTO_INCREMENT,
    SocialSecNr VARCHAR(15),
    Customer_ID INT NULL,
    Admin_ID INT NULL,
    FOREIGN KEY (Customer_ID) REFERENCES customer(Customer_ID),
    FOREIGN KEY (Admin_ID) REFERENCES admin(Admin_ID)
);
```

## Code example for above example for assignment 2 b - admin roles
  
```sql
CREATE TABLE admin_roles (
    Role_ID INT PRIMARY KEY AUTO_INCREMENT,
    Role_name VARCHAR(50)
);
```

## Code example for above example for assignment 2 b - admin permissions
  
```sql
CREATE TABLE admin_role_permissions (
    Admin_ID INT,
    Role_ID INT,
    FOREIGN KEY (Admin_ID) REFERENCES admin(Admin_ID),
    FOREIGN KEY (Role_ID) REFERENCES admin_roles(Role_ID),
    PRIMARY KEY (Admin_ID, Role_ID)
);
```

## Code example for above example for assignment 3 a - example 1, category and embedded actor

```json
{
  "_id": ObjectId("..."),
  "title": "Inception",
  "director": "Christopher Nolan",
  "storyDescription": "A thief with the ability to enter people's dreams...",
  "actors": [
    {
      "actor_id": ObjectId("..."),
      "firstname": "Leonardo",
      "lastname": "DiCaprio",
      "birthdate": "1974-11-11"
    },
    {
      "actor_id": ObjectId("..."),
      "firstname": "Joseph",
      "lastname": "Gordon-Levitt",
      "birthdate": "1981-02-17"
    }
  ],
  "categories": ["Sci-Fi", "Action"]
}
```
  
## Code example for above example for assignment 3 a - example 2, customer and ticket
  
```json
{
  "_id": ObjectId("..."),
  "firstname": "John",
  "lastname": "Doe",
  "socialSecNr": "1234567890",
  "tickets": [
    {
      "movie_id": ObjectId("..."),
      "movie_title": "Inception",
      "price": 120,
      "purchaseDate": "2024-01-15"
    },
    {
      "movie_id": ObjectId("..."),
      "movie_title": "The Matrix",
      "price": 110,
      "purchaseDate": "2024-02-10"
    }
  ]
}
```

## Code example for above example for assignment 3 b - actor-search through all movies
  
```javascript
db.movie.find(
  { "actors.actor_firstname": "Leonardo", "actors.actor_lastname": "DiCaprio" },
  { "title": 1, "actors.$": 1 }
)
``` 
  