**F1 Race SQL Challenge**  
Download the table and schema to follow the challenge

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
