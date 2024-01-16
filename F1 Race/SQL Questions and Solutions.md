**F1 Race SQL Challenge**

**Question 1**/n
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

