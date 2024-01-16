**F1 Race SQL Challenge**  
*Download the table and schema to follow the challenge*

**Question 1**  
Return the list of drivers Driver First Name LAst Name and limit to first 10 records

	SELECT DRIVERID,
	FORENAME AS First_Name,
	SURNAME AS Last_Name
	FROM DRIVERS
	LIMIT 10;
  
  **Result**
  
|DRIVERID|FIRST_NAME|LAST_NAME |
|--------|----------|----------|
|1       |Lewis     |Hamilton  |
|856     |Nyck      |de Vries  |
|855     |Guanyu    |Zhou      |
|854     |Mick      |Schumacher|
|853     |Nikita    |Mazepin   |
|852     |Yuki      |Tsunoda   |
|851     |Jack      |Aitken    |
|850     |Pietro    |Fittipaldi|
|849     |Nicholas  |Latifi    |
|848     |Alexander |Albon     |

<br>
<br>
<br>
    
**Question 2**  
Return the list of drivers and their fastest lap speed. Limit to 10 records.

	SELECT d.DRIVERID,
	    d.FORENAME AS First_Name,
	    d.SURNAME AS Last_Name,
	    r.fastestlapspeed
	FROM DRIVERS as d
	JOIN RESULTS as r
	    ON d.driverid = r.driverid
	WHERE r.fastestlapspeed is not null 
	ORDER BY d.driverid
	LIMIT 10
	;

 **Result**

|DRIVERID|FIRST_NAME|LAST_NAME |FASTESTLAPSPEED|
|--------|----------|----------|---------------|
|1       |Lewis     |Hamilton  |218.3          |
|1       |Lewis     |Hamilton  |205.022        |
|1       |Lewis     |Hamilton  |222.085        |
|1       |Lewis     |Hamilton  |193.533        |
|1       |Lewis     |Hamilton  |199.398        |
|1       |Lewis     |Hamilton  |153.152        |
|1       |Lewis     |Hamilton  |204.323        |
|1       |Lewis     |Hamilton  |197.285        |
|1       |Lewis     |Hamilton  |216.552        |
|1       |Lewis     |Hamilton  |209.033        |

<br>
<br>
<br>

**Question 3**  
Return the list of drivers and their fastest lap speed ever, Limit to 10

	SELECT d.driverid,
	forename as First_Name,
	surname as Last_Name,
	MAX(fastestlapspeed) as Fastest_Lap_Speed_Ever 
	FROM drivers as d
	INNER JOIN results as r ON d.driverid = r.driverid
	WHERE fastestlapspeed IS NOT NULL
	GROUP BY d.driverid,
	forename,
	surname;

**Result**
|DRIVERID|FIRST_NAME|LAST_NAME |FASTEST_LAP_SPEED_EVER|
|--------|----------|----------|----------------------|
|1       |Lewis     |Hamilton  |255.014               |
|2       |Nick      |Heidfeld  |250.375               |
|3       |Nico      |Rosberg   |246.884               |
|4       |Fernando  |Alonso    |253.874               |
|5       |Heikki    |Kovalainen|247.605               |
|8       |Kimi      |Räikkönen |255.874               |
|9       |Robert    |Kubica    |250.927               |
|14      |David     |Coulthard |251.599               |
|18      |Jenson    |Button    |252.262               |
|13      |Felipe    |Massa     |251.441               |

<br>
<br>
<br>

**Question 4**  
Return the list of drivers and their fastest lap speed in Monaco in 2021

	SELECT d.driverid, 
	forename, 
	surname, 
	MAX(fastestlapspeed) as Fastest_Lap_Speed_in_Monaco_2021 
	FROM drivers as d
	INNER JOIN results as r ON d.driverid = r.driverid
	INNER JOIN races as races ON r.raceid = races.raceid
	WHERE fastestlapspeed IS NOT NULL
	AND races.year = 2021
	AND races.name LIKE '%Monaco%'
	GROUP BY d.driverid, forename, surname;

 **Result**
 |DRIVERID|FORENAME |SURNAME   |FASTEST_LAP_SPEED_IN_MONACO_2021|
|--------|---------|----------|--------------------------------|
|1       |Lewis    |Hamilton  |164.769                         |
|853     |Nikita   |Mazepin   |156.287                         |
|852     |Yuki     |Tsunoda   |162.259                         |
|849     |Nicholas |Latifi    |158.961                         |
|847     |George   |Russell   |159.033                         |
|841     |Antonio  |Giovinazzi|159.472                         |
|839     |Esteban  |Ocon      |159.503                         |
|832     |Carlos   |Sainz     |160.989                         |
|830     |Max      |Verstappen|160.929                         |
|822     |Valtteri |Bottas    |158.682                         |
|817     |Daniel   |Ricciardo |161.082                         |
|846     |Lando    |Norris    |160.883                         |
|840     |Lance    |Stroll    |160.875                         |
|20      |Sebastian|Vettel    |159.503                         |
|8       |Kimi     |Räikkönen |160.237                         |
|854     |Mick     |Schumacher|157.189                         |
|842     |Pierre   |Gasly     |159.3                           |
|815     |Sergio   |Pérez     |161.138                         |
|4       |Fernando |Alonso    |160.12                          |

<br>
<br>
<br>

**Question 5**  
Return the list of drivers and their fastest lap speed in Monaco in 2021, as well as the fastest lap speed of all time

	SELECT d.driverid, 
	forename, 
	surname, 
	MAX(fastestlapspeed) as Fastest_Lap_Speed_in_Monaco_2021,
	(SELECT MAX(fastestlapspeed) FROM results) as All_Time_Fastest_LS
	FROM drivers as d
	INNER JOIN results as r ON d.driverid = r.driverid
	INNER JOIN races as races ON r.raceid = races.raceid
	WHERE fastestlapspeed IS NOT NULL
	AND races.year = 2021
	AND races.name LIKE '%Monaco%'
	GROUP BY d.driverid, forename, surname;

 **Results**
 |DRIVERID|FORENAME |SURNAME   |FASTEST_LAP_SPEED_IN_MONACO_2021|ALL_TIME_FASTEST_LS|
|--------|---------|----------|--------------------------------|-------------------|
|1       |Lewis    |Hamilton  |164.769                         |257.32             |
|853     |Nikita   |Mazepin   |156.287                         |257.32             |
|852     |Yuki     |Tsunoda   |162.259                         |257.32             |
|849     |Nicholas |Latifi    |158.961                         |257.32             |
|847     |George   |Russell   |159.033                         |257.32             |
|841     |Antonio  |Giovinazzi|159.472                         |257.32             |
|839     |Esteban  |Ocon      |159.503                         |257.32             |
|832     |Carlos   |Sainz     |160.989                         |257.32             |
|830     |Max      |Verstappen|160.929                         |257.32             |
|822     |Valtteri |Bottas    |158.682                         |257.32             |
|817     |Daniel   |Ricciardo |161.082                         |257.32             |
|846     |Lando    |Norris    |160.883                         |257.32             |
|840     |Lance    |Stroll    |160.875                         |257.32             |
|20      |Sebastian|Vettel    |159.503                         |257.32             |
|8       |Kimi     |Räikkönen |160.237                         |257.32             |
|854     |Mick     |Schumacher|157.189                         |257.32             |
|842     |Pierre   |Gasly     |159.3                           |257.32             |
|815     |Sergio   |Pérez     |161.138                         |257.32             |
|4       |Fernando |Alonso    |160.12                          |257.32             |

<br>
<br>
<br>

**Question 6**  
Return the list of drivers, their fastest lap speed in Monaco in 2021, as well as how many times they have won in Monaco in total

	SELECT d.driverid, 
	forename, 
	surname, 
	MAX(fastestlapspeed) as Fastest_Lap_Speed_in_Monaco_2021,
	SUM(total_wins)
	FROM drivers as d
	INNER JOIN results as r ON d.driverid = r.driverid
	INNER JOIN races as races ON r.raceid = races.raceid
	INNER JOIN (SELECT driverid, SUM(wins) as total_wins, name
				FROM driver_standings as ds
				INNER JOIN races as r on r.raceid = ds.raceid
				WHERE name LIKE '%Monaco%'
	GROUP BY driverid, name) as wins ON d.driverid = wins.driverid
	WHERE fastestlapspeed IS NOT NULL
	AND races.year = 2021
	AND races.name LIKE '%Monaco%'
	GROUP BY d.driverid, forename, surname;

 **Result**
 |DRIVERID|FORENAME |SURNAME   |FASTEST_LAP_SPEED_IN_MONACO_2021|SUM(TOTAL_WINS)|
|--------|---------|----------|--------------------------------|---------------|
|832     |Carlos   |Sainz     |160.989                         |0              |
|830     |Max      |Verstappen|160.929                         |7              |
|846     |Lando    |Norris    |160.883                         |0              |
|815     |Sergio   |Pérez     |161.138                         |1              |
|20      |Sebastian|Vettel    |159.503                         |16             |
|842     |Pierre   |Gasly     |159.3                           |0              |
|1       |Lewis    |Hamilton  |164.769                         |22             |
|840     |Lance    |Stroll    |160.875                         |0              |
|839     |Esteban  |Ocon      |159.503                         |0              |
|841     |Antonio  |Giovinazzi|159.472                         |0              |
|817     |Daniel   |Ricciardo |161.082                         |2              |
|849     |Nicholas |Latifi    |158.961                         |0              |
|852     |Yuki     |Tsunoda   |162.259                         |0              |
|853     |Nikita   |Mazepin   |156.287                         |0              |
|854     |Mick     |Schumacher|157.189                         |0              |
|822     |Valtteri |Bottas    |158.682                         |3              |
|8       |Kimi     |Räikkönen |160.237                         |7              |
|847     |George   |Russell   |159.033                         |0              |
|4       |Fernando |Alonso    |160.12                          |13             |

<br>
<br>
<br>




	


