# SQL Game: [sqlnoir.com](https://www.sqlnoir.com/)

<!-- Preface -->

> YouTube Streaming: [Click here](https://youtube.com/live/vqgh0E-_Hx8?feature=share).

<div style="page-break-after: always;"></div>

## Case #003: The Miami Marina Murder

A body was found floating near the docks of Coral Bay Marina in the early hours of August 14, 1986. Your job, detective, is to find the murderer and bring them to justice. This case might require the use of JOINs, wildcard searches, and logical deduction. Get to work, detective.

## Objectives

    1.Find the murderer. ( Start by finding the crime scene and go from there )

## General Information: `crime_scene`
```sql
select * From crime_scene
where date='19860814'
and location like 'coral%'
```

|id|	date|	location|	description|
|--|--|--|--|
|43|	19860814|	Coral Bay Marina|	The body of an unidentified man was found near the docks. Two people were seen nearby: one who lives on 300ish "Ocean Drive" and another whose first name ends with "ul" and his last name ends with "ez".|
|

> Information based on description:
1. 2 people.
2. 300ish "Ocean Drive"
3. first name ends with "ul", last name ends with "ez"

```sql
select * from person
where address like '3% %ocean%'
```

|id|	name|	alias|	occupation|	address|
|--|--|--|--|--|
|5|	Michael Santos|	Silent Mike|	Bartender|	33 Ocean Drive|
|95|	Herman Cunningham|	The Hammer|	Construction Foreman|	321 Ocean Lane|
|101|	Carlos Mendez|	Los Ojos|	Fisherman|	369 Ocean Drive|
|105|	Victor Martinez|	Slick Vic|	Bartender|	33 Ocean Drive|
|

> Now we can suspect one people, which `Carlos Mendez ` because address on 3xx Ocean Drive. Then we just need to find another one.

```sql
select * from person
where name like '%ul %ez'
```

|id|	name|	alias|	occupation|	address|
|--|--|--|--|--|
|102|	Raul Gutierrez|	The Cobra|	Nightclub Owner|	45 Sunset Ave|
|

> We now have 2 names, and the 2nd one is `Raul Gutierrez`.

## Find the truth through the `interviews`
```sql
select * from interviews
where person_id in('101','102')
```

|id|	person_id|	transcript|
|--|--|--|
|101|	101|	I saw someone check into a hotel on August 13. The guy looked nervous.|
|103|	102|	I heard someone checked into a hotel with "Sunset" in the name.|
|

>From both information, we can find more deeper information. 1st, <b>hotel checkin on Aug 13</b>, 2nd  <b>"Sunset" in the name</b>, 3rd <b>man</b>.

### Temp query for get person_id from `hotel_checkins`
```sql
select*from hotel_checkins
where check_in_date like '%0813'
and hotel_name like '%sunset%'
```

