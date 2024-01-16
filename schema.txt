INSERT INTO location (city, state, country) VALUES ('Nashville', 'Tennessee','United States'),('Memphis','Tennessee','United States'),('Phoenix','Arizona','United States'),('Denver','Colorado','United States');

INSERT INTO person ("firstName", "lastName", age, location_id) VALUES ('Chickie', 'Ourtic', 21, 1),('Hilton', 'O''Hanley', 37, 1), ('Barbe', 'Purver', 50, 3), ('Reeta', 'Sammons', 34, 2), ('Abbott', 'Fisbburne', 49, 1), ('Winnie', 'Whines', 19, 4),('Samantha', 'Leese', 35, 2), ('Edouard', 'Lorimer', 29, 1), ('Mattheus', 'Shaplin', 27, 3),  ('Donnell', 'Corney', 25, 3), ('Wallis', 'Kauschke', 28, 3), ('Melva', 'Lanham', 20, 2), ('Amelina', 'McNirlan', 22, 4),  ('Courtney', 'Holley', 22, 1), ('Sigismond', 'Vala', 21, 4), ('Jacquelynn', 'Halfacre', 24, 2), ('Alanna', 'Spino', 25, 3), ('Isa', 'Slight', 32, 1), ('Kakalina', 'Renne', 26, 3);

INSERT INTO interest (title) VALUES ('Programming'),('Gaming'),('Computers'),('Music'),('Movies'),('Cooking'), ('Sports');

INSERT INTO person_interest (person_id,interest_id) VALUES (1,1),(1,2),(1,6),(2,1),(2,7),(2,4),(3,1),(3,3),(3,4),(4,1),(4,2),(4,7),(5,6),(5,3),(5,4),(6,2),(6,7),(7,1),(7,3),(8,2),(8,4),(9,5),(9,6),(10,7),(10,5),(11,1),(11,2),(11,5),(12,1),(12,4),(12,5),(13,2),(13,3),(13,7),(14,2),(14,4),(14,6),(15,1),(15,5),(15,7),(16,2),(16,3),(16,4),(17,1),(17,3),(17,5),(17,7),(18,2),(18,4),(18,6),(19,1),(19,2),(19,3),(19,4),(19,5),(19,6),(19,7);

UPDATE person SET age = age + 1 WHERE id = 1 OR id = 6 OR id = 8 OR id = 14 OR id = 12 OR id = 18 OR id = 5 OR id = 4;

DELETE FROM person_interest WHERE person_id = 2 OR person_id = 17;
DELETE FROM person WHERE id = 2 OR id = 17;

SELECT "firstName", "lastName" FROM person;

SELECT "firstName", "lastName", city, state FROM person 
JOIN location ON person.location_id = location.id 
WHERE city = 'Nashville' AND state = 'Tennessee';

SELECT city, COUNT(city) FROM location
JOIN person ON person.location_id = location.id
GROUP BY city;

SELECT title, COUNT(person_interest.person_id) FROM interest
JOIN person_interest ON person_interest.interest_id = interest.id
GROUP BY title;

SELECT "firstName", "lastName", city, state, interest.title AS interest FROM person
JOIN location ON person.location_id = location.id
JOIN person_interest ON person.id = person_interest.person_id
JOIN interest ON person_interest.interest_id = interest.id;

SELECT CASE WHEN AVG(age) BETWEEN 20 AND 30 THEN '20-30'
WHEN AVG(age) BETWEEN 31 AND 40 THEN '30-40'
WHEN AVG(age) BETWEEN 41 AND 50 THEN '40-50' end as range, count(age) FROM person
GROUP BY
CASE WHEN age BETWEEN 20 AND 30 then 1 else 0 end,
CASE WHEN age BETWEEN 31 AND 40 then 1 else 0 end,
CASE WHEN age BETWEEN 41 AND 50 then 1 else 0 end
ORDER BY AVG(age);