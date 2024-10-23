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
  