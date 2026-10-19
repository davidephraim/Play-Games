# SQL Game: [sqlnoir.com](https://www.sqlnoir.com/)

<!-- Preface -->

> YouTube Streaming: [Click here](https://youtube.com/live/vqgh0E-_Hx8?feature=share).

<div style="page-break-after: always;"></div>

## Case #002: The Stolen Sound

>In the neon glow of 1980s Los Angeles, the West Hollywood Records store was rocked by a daring theft. A prized vinyl record, worth over $10,000, vanished during a busy evening, leaving the store owner desperate for answers. Vaguely recalling the details, you know the incident occurred on July 15, 1983, at this famous store. Your task is to track down the thief and bring them to justice.

## Objectives

    1.Retrieve the crime scene report for the record theft using the known date and location.
    2.Retrieve witness records linked to that crime scene to obtain their clues.
    3.Use the clues from the witnesses to find the suspect in the suspects table.
    4.Retrieve the suspect's interview transcript to confirm the confession.

## Gathering Information: `crime_scene`
```sql
select * from crime_scene
where type='theft'
and date='19830715'
```

|id|	date|	type|	location|	description|
|--|--|--|--|--|
|65|	19830715|	theft|	West Hollywood Records|	A prized vinyl record was stolen from the store during a busy evening.|
|

## Search for the witness(es)
```sql
select * from witnesses
where crime_scene_id=65
```

|id|	crime_scene_id|	clue|
|--|--|--|
|28|	65|	I saw a man wearing a red bandana rushing out of the store.|
|75|	65|	The main thing I remember is that he had a distinctive gold watch on his wrist.|
|

> There are two witnesses. 1st saw <b> a man, red bandana</b>. 2nd remembered a man had a distinctive <b>gold watch on his wrist</b>.

## Search `suspects` based on witnesses clues
```sql
select * from suspects
where bandana_color='red'
and accessory like 'gold watch'
```

|id|	name|	bandana_color|	accessory|
|--|--|--|--|
|35|	Tony Ramirez|	red|	gold watch|
|44|	Mickey Rivera|	red|	gold watch|
|97|	Rico Delgado|	red|	gold watch|
|

## Get the transcript from `interviews` based on 3 suspects
```sql
select * from interviews
where suspect_id in(35,44,97)
```

|suspect_id|	transcript|
|--|--|
|35|	I wasn't anywhere near West Hollywood Records that night.|
|44|	I was busy with my music career; I have nothing to do with this theft.|
|97|	I couldn't help it. I snapped and took the record.|
|

> Based on the transcript, we can surely know that id `97` as the `theft`.

## Submission
```sql
select * from suspects
where id=97
```

|id|	name|	bandana_color|	accessory|
|--|--|--|--|
|97|	Rico Delgado|	red|	gold watch|
|

## Result

>Case Closed\
Case Solved!
\
Excellent work, detective! Rico Delgado has confessed to stealing the prized vinyl record.