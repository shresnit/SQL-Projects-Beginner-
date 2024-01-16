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
**Question 3**  
Return the list of drivers and their fastest lap speed ever

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
|10      |Timo      |Glock     |243.201               |
|22      |Rubens    |Barrichello|257.32                |
|20      |Sebastian |Vettel    |252.77                |
|17      |Mark      |Webber    |251.459               |
|6       |Kazuki    |Nakajima  |242.565               |
|7       |Sébastien |Bourdais  |233.646               |
|25      |Alexander |Wurz      |245.35                |
|30      |Michael   |Schumacher|256.324               |
|31      |Juan      |Pablo Montoya|254.861               |
|32      |Christian |Klien     |249.961               |
|27      |Christijan|Albers    |245.448               |
|37      |Pedro     |de la Rosa|249.155               |
|36      |Franck    |Montagny  |212.323               |
|39      |Narain    |Karthikeyan|244.929               |
|47      |Zsolt     |Baumgartner|241.497               |
|154     |Romain    |Grosjean  |245.972               |
|69      |Luca      |Badoer    |229.633               |
|814     |Paul      |di Resta  |236.841               |
|813     |Pastor    |Maldonado |239.762               |
|823     |Giedo     |van der Garde|235.214               |
|834     |Alexander |Rossi     |206.029               |
|838     |Stoffel   |Vandoorne |246.79                |
|812     |Karun     |Chandhok  |214.656               |
|822     |Valtteri  |Bottas    |251.69                |
|849     |Nicholas  |Latifi    |245.353               |
|854     |Mick      |Schumacher|244.493               |
|16      |Adrian    |Sutil     |246.106               |
|23      |Ralf      |Schumacher|251.032               |
|24      |Vitantonio|Liuzzi    |246.033               |
|28      |Markus    |Winkelhock|180.309               |
|44      |Olivier   |Panis     |233.04                |
|41      |Ricardo   |Zonta     |250.027               |
|817     |Daniel    |Ricciardo |250.174               |
|816     |Jérôme    |d'Ambrosio|235.177               |
|824     |Jules     |Bianchi   |232.767               |
|825     |Kevin     |Magnussen |248.959               |
|845     |Sergey    |Sirotkin  |246.568               |
|843     |Brendon   |Hartley   |239.685               |
|853     |Nikita    |Mazepin   |239.155               |
|844     |Charles   |Leclerc   |251.235               |
|837     |Rio       |Haryanto  |221.398               |
|847     |George    |Russell   |247.033               |
|15      |Jarno     |Trulli    |251.775               |
|21      |Giancarlo |Fisichella|252.519               |
|11      |Takuma    |Sato      |252.296               |
|29      |Sakon     |Yamamoto  |243.978               |
|33      |Tiago     |Monteiro  |245.9                 |
|34      |Yuji      |Ide       |203.663               |
|35      |Jacques   |Villeneuve|248.591               |
|42      |Antônio   |Pizzonia  |253.566               |
|38      |Robert    |Doornbos  |244.794               |
|40      |Patrick   |Friesacher|213.987               |
|43      |Cristiano |da Matta  |229.145               |
|67      |Sébastien |Buemi     |244.705               |
|818     |Jean-Éric |Vergne    |234.005               |
|832     |Carlos    |Sainz     |249.671               |
|848     |Alexander |Albon     |250.165               |
|829     |Will      |Stevens   |228.927               |
|831     |Felipe    |Nasr      |235.24                |
|810     |Lucas     |di Grassi |236.526               |
|855     |Guanyu    |Zhou      |241.484               |
|19      |Anthony   |Davidson  |245.016               |
|26      |Scott     |Speed     |245.079               |
|45      |Giorgio   |Pantano   |248.091               |
|46      |Gianmaria |Bruni     |241.456               |
|153     |Jaime     |Alguersuari|243.995              |
|807     |Nico      |Hülkenberg|249.337               |
|808     |Vitaly    |Petrov    |246.382               |
|811     |Bruno     |Senna     |240                   |
|819     |Charles   |Pic       |235.328               |
|821     |Esteban   |Gutiérrez |239.457               |
|820     |Max       |Chilton   |233.037               |
|828     |Marcus    |Ericsson  |246.024               |
|839     |Esteban   |Ocon      |247.555               |
|842     |Pierre    |Gasly     |248.611               |
|846     |Lando     |Norris    |248.141               |
|841     |Antonio   |Giovinazzi|246.793               |
|840     |Lance     |Stroll    |248.576               |
|856     |Nyck      |de Vries  |240.75                |
|836     |Pascal    |Wehrlein  |240.965               |
|833     |Roberto   |Merhi     |228.393               |
|826     |Daniil    |Kvyat     |246.863               |
|851     |Jack      |Aitken    |222.24                |
|850     |Pietro    |Fittipaldi|220.892               |
|815     |Sergio    |Pérez     |248.953               |
|835     |Jolyon    |Palmer    |243.198               |
|12      |Nelson    |Piquet Jr.|229.38                |
|155     |Kamui     |Kobayashi |234.239               |
|830     |Max       |Verstappen|250.83                |
|48      |Marc      |Gené      |230.096               |
|852     |Yuki      |Tsunoda   |240.269               |

<br>
<br>

