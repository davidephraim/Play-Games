# SQL Game: [sqlnoir.com](https://www.sqlnoir.com/)

<!-- Preface -->

> YouTube Streaming: [Click here](https://youtube.com/live/xh1A2-qEEgI?feature=share).

<div style="page-break-after: always;"></div>

## Case #001: The Vanishing Briefcase
> Set in the gritty 1980s, a valuable briefcase has disappeared from the Blue Note Lounge. A witness reported that a man in a trench coat was seen fleeing the scene. Investigate the crime scene, review the list of suspects, and examine interview transcripts to reveal the culprit.

## Objectives

    1.Retrieve the correct crime scene details to gather the key clue.
    2.Identify the suspect whose profile matches the witness description.
    3.Verify the suspect using their interview transcript.

## Gathering Information: Place and type from `crime_scene`
```sql
select * from crime_scene
where type='theft'
and location like 'blue note %'
```

|id|	date|	type|	location|	description|
|--|--|--|--|--|
|76|	19851120|	theft|	Blue Note Lounge|	A briefcase containing sensitive documents vanished. A witness reported a man in a trench coat with a scar on his left cheek fleeing the scene.|
|

1. Man
2. Trench coat
3. Left cheeck scar

```sql
select * from suspects
where attire like 'trench %'
and scar like 'left%'
```

|id|	name|	attire|	scar|
|--|--|--|--|
|3|	Frankie Lombardi|	trench coat|	left cheek|
|183|	Vincent Malone|	trench coat|	left cheek|
|

Now we have two suspects with id <b>3</b> and <b>183</b>.
```sql
select * from interviews
where suspect_id=3 and transcript not null
or suspect_id=183 and transcript not null
```

|suspect_id|	transcript|
|--|--|
|183|	I wasn’t going to steal it, but I did.|
|

Now we can surely know that <b>Vincent Malone</b> has done a crime.
