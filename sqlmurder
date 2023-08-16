# The SQL code I used to solve SQL Murder Mystery: https://mystery.knightlab.com/
# I used an Excel page to temporarily store the data obtained from quaries

# To find the descripion of the murder:
SELECT * 
	FROM crime_scene_report
	WHERE date = 20180115
	AND type = "murder"
	AND city = "SQL City";

# To find the witnesses:
SELECT * 
	FROM person
	WHERE address_street_name = "Franklin Ave" 
	AND name LIKE "%Annabel%"
	OR address_number = (
		SELECT max(address_number)
			FROM person);

# To read the witnesses stories:
SELECT * 
	FROM interview
	WHERE person_id IN (14887, 16371);

# To get the fitness member IDs of witnesses
SELECT id, person_id, name
	FROM get_fit_now_member
	WHERE person_id IN (14887, 16371);

# Getting each persons IDs who checked in 9 Jul. 2018 and filter with the membership number on the bag
SELECT gfc.membership_id, gfc.check_in_date, p.id, p.name
	FROM person p 
	JOIN get_fit_now_member gfm ON gfm.person_id = p.id
	JOIN get_fit_now_check_in gfc ON gfc.membership_id = gfm.id
	WHERE gfc.check_in_date = 20180109
	AND gfc.membership_id LIKE "%48Z%";

# To find the driver (and therefore the murderer) [Jeremy Bowers]
SELECT d.id, p.name, p.license_id, d.plate_number
	FROM drivers_license d
	JOIN person p ON p.license_id = d.id
	WHERE p.id IN (28819, 67318)
	AND plate_number LIKE "%H42W%";

#To find the villain planned all of this
## To read the murderers transcript
SELECT *
	FROM interview
	WHERE person_id = 67318;

## To find the villain [Miranda Priestly]
SELECT fec.person_id, p.name, fec.event_name, d.height
	FROM facebook_event_checkin fec
	JOIN drivers_license d ON d.id = p.license_id
	JOIN person p ON p.id = fec.person_id
	WHERE fec.event_name LIKE "%SQL%"
	AND fec.date BETWEEN 20171201 AND 20171231
	AND d.height BETWEEN 65 AND 67
	AND d.hair_color = "red";
