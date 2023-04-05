```python
# importing libraries

import pandas as pd
import sqlite3
```


```python
# installing the ipython-sql library
!pip install ipython-sql
```


```python
#importing a dataframe to import data

df = pd.read_excel('Lown_Hospital Index.xlsx')
```


```python
#Create a Connection

cnn = sqlite3.connect ('lown_hospital.db')
```


```python
df.to_sql('hospital_ranking', cnn)
```


```python
# Load the sql module to ipython

%load_ext sql
```


```python
%sql sqlite:///lown_hospital.db
```


```python
print (df.columns.values)
```

    ['RECORD_ID' 'Name' 'State' 'City' 'Address' 'Zip' 'Size' 'TYPE_ForProfit'
     'TYPE_NonProfit' 'TYPE_chrch_affl_f' 'TYPE_urban' 'TYPE_rural'
     'Tier 1_Lown Composite Overall Rank'
     'Tier 1_Lown Composite Overall Grade' 'Tier 2_Equity Overall Rank'
     'Tier 2_Equity Overall Grade' 'Tier 3_Pay Equity Rank'
     'Tier 3_Community Benefit Rank' 'Tier 3_Inclusivity Rank'
     'Tier 3_Pay Equity Grade' 'Tier 3_Community Benefit Grade'
     'Tier 3_Inclusivity Grade' 'Attribute']
    

## SQL Exercise

Q1. How many hospitals are in each state?


```sql
%%sql

SELECT State
    , COUNT(RECORD_ID)
FROM hospital_ranking
GROUP BY State
ORDER BY State
;
```

     * sqlite:///lown_hospital.db
    Done.
    




<table>
    <thead>
        <tr>
            <th>State</th>
            <th>COUNT(RECORD_ID)</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>AK</td>
            <td>14</td>
        </tr>
        <tr>
            <td>AL</td>
            <td>88</td>
        </tr>
        <tr>
            <td>AR</td>
            <td>76</td>
        </tr>
        <tr>
            <td>AZ</td>
            <td>63</td>
        </tr>
        <tr>
            <td>CA</td>
            <td>283</td>
        </tr>
        <tr>
            <td>CO</td>
            <td>73</td>
        </tr>
        <tr>
            <td>CT</td>
            <td>32</td>
        </tr>
        <tr>
            <td>DC</td>
            <td>10</td>
        </tr>
        <tr>
            <td>DE</td>
            <td>7</td>
        </tr>
        <tr>
            <td>FL</td>
            <td>188</td>
        </tr>
        <tr>
            <td>GA</td>
            <td>135</td>
        </tr>
        <tr>
            <td>HI</td>
            <td>15</td>
        </tr>
        <tr>
            <td>IA</td>
            <td>114</td>
        </tr>
        <tr>
            <td>ID</td>
            <td>39</td>
        </tr>
        <tr>
            <td>IL</td>
            <td>187</td>
        </tr>
        <tr>
            <td>IN</td>
            <td>122</td>
        </tr>
        <tr>
            <td>KS</td>
            <td>104</td>
        </tr>
        <tr>
            <td>KY</td>
            <td>100</td>
        </tr>
        <tr>
            <td>LA</td>
            <td>88</td>
        </tr>
        <tr>
            <td>MA</td>
            <td>66</td>
        </tr>
        <tr>
            <td>MD</td>
            <td>53</td>
        </tr>
        <tr>
            <td>ME</td>
            <td>36</td>
        </tr>
        <tr>
            <td>MI</td>
            <td>127</td>
        </tr>
        <tr>
            <td>MN</td>
            <td>119</td>
        </tr>
        <tr>
            <td>MO</td>
            <td>110</td>
        </tr>
        <tr>
            <td>MS</td>
            <td>82</td>
        </tr>
        <tr>
            <td>MT</td>
            <td>35</td>
        </tr>
        <tr>
            <td>NC</td>
            <td>112</td>
        </tr>
        <tr>
            <td>ND</td>
            <td>29</td>
        </tr>
        <tr>
            <td>NE</td>
            <td>72</td>
        </tr>
        <tr>
            <td>NH</td>
            <td>32</td>
        </tr>
        <tr>
            <td>NJ</td>
            <td>74</td>
        </tr>
        <tr>
            <td>NM</td>
            <td>39</td>
        </tr>
        <tr>
            <td>NV</td>
            <td>35</td>
        </tr>
        <tr>
            <td>NY</td>
            <td>167</td>
        </tr>
        <tr>
            <td>OH</td>
            <td>156</td>
        </tr>
        <tr>
            <td>OK</td>
            <td>90</td>
        </tr>
        <tr>
            <td>OR</td>
            <td>65</td>
        </tr>
        <tr>
            <td>PA</td>
            <td>163</td>
        </tr>
        <tr>
            <td>RI</td>
            <td>13</td>
        </tr>
        <tr>
            <td>SC</td>
            <td>61</td>
        </tr>
        <tr>
            <td>SD</td>
            <td>38</td>
        </tr>
        <tr>
            <td>TN</td>
            <td>100</td>
        </tr>
        <tr>
            <td>TX</td>
            <td>291</td>
        </tr>
        <tr>
            <td>UT</td>
            <td>41</td>
        </tr>
        <tr>
            <td>VA</td>
            <td>90</td>
        </tr>
        <tr>
            <td>VT</td>
            <td>15</td>
        </tr>
        <tr>
            <td>WA</td>
            <td>78</td>
        </tr>
        <tr>
            <td>WI</td>
            <td>132</td>
        </tr>
        <tr>
            <td>WV</td>
            <td>45</td>
        </tr>
        <tr>
            <td>WY</td>
            <td>21</td>
        </tr>
    </tbody>
</table>



 

Q2. Which State has the most hospital?


```sql
%%sql

SELECT State
    , COUNT(DISTINCT Name) AS 'Number of Hospital'
FROM hospital_ranking
GROUP BY State
ORDER BY COUNT(Name) DESC
LIMIT 1
;
```

     * sqlite:///lown_hospital.db
    Done.
    




<table>
    <thead>
        <tr>
            <th>State</th>
            <th>Number of Hospital</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>TX</td>
            <td>288</td>
        </tr>
    </tbody>
</table>



 

Q3. What is the distribution of community benefit grades across all hospitals?


```sql
%%sql

SELECT [Tier 3_Community Benefit Grade] AS "Community Benefit Grades"
    ,COUNT( DISTINCT [RECORD_ID]) As "Number of Hospitals"
FROM hospital_ranking
GROUP BY [Tier 3_Community Benefit Grade]
HAVING [Tier 3_Community Benefit Grade] NOT NULL
;



```

     * sqlite:///lown_hospital.db
    Done.
    




<table>
    <thead>
        <tr>
            <th>Community Benefit Grades</th>
            <th>Number of Hospitals</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>A</td>
            <td>950</td>
        </tr>
        <tr>
            <td>B</td>
            <td>1453</td>
        </tr>
        <tr>
            <td>C</td>
            <td>1005</td>
        </tr>
        <tr>
            <td>D</td>
            <td>579</td>
        </tr>
    </tbody>
</table>



 

Include at least the Name, City, and State of the hospital and sort the table by the hospital’s overall rank, “Lown Composite Overall Rank,” 


```sql
%%sql

SELECT Name
    , City
    , State
    , [Tier 1_Lown Composite Overall Rank] AS "Composite Overall Rank"
FROM hospital_ranking
WHERE [Tier 1_Lown Composite Overall Rank] IS NOT NULL
GROUP BY Name
ORDER BY [Composite Overall Rank]
;
```

     * sqlite:///lown_hospital.db
    Done.
    




<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>City</th>
            <th>State</th>
            <th>Composite Overall Rank</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Adventist Health Howard Memorial</td>
            <td>Willits</td>
            <td>CA</td>
            <td>1.0</td>
        </tr>
        <tr>
            <td>Queen&#x27;s Health Systems</td>
            <td>None</td>
            <td>HI</td>
            <td>1.0</td>
        </tr>
        <tr>
            <td>Duke Regional Hospital</td>
            <td>Durham</td>
            <td>NC</td>
            <td>2.0</td>
        </tr>
        <tr>
            <td>UCHealth (Colorado)</td>
            <td>None</td>
            <td>CO</td>
            <td>2.0</td>
        </tr>
        <tr>
            <td>St. Lukes University Health Network</td>
            <td>None</td>
            <td>NJ</td>
            <td>3.0</td>
        </tr>
        <tr>
            <td>Tristar Horizon Medical Center</td>
            <td>Dickson</td>
            <td>TN</td>
            <td>3.0</td>
        </tr>
        <tr>
            <td>Boston Medical Center Corporation</td>
            <td>Boston</td>
            <td>MA</td>
            <td>4.0</td>
        </tr>
        <tr>
            <td>North Memorial Health Care</td>
            <td>None</td>
            <td>MN</td>
            <td>4.0</td>
        </tr>
        <tr>
            <td>Nebraska Medicine</td>
            <td>None</td>
            <td>NE</td>
            <td>5.0</td>
        </tr>
        <tr>
            <td>Salinas Valley Memorial Hospital</td>
            <td>Salinas</td>
            <td>CA</td>
            <td>5.0</td>
        </tr>
        <tr>
            <td>Legacy Mount Hood Medical Center</td>
            <td>Gresham</td>
            <td>OR</td>
            <td>6.0</td>
        </tr>
        <tr>
            <td>Sutter Health</td>
            <td>None</td>
            <td>CA</td>
            <td>6.0</td>
        </tr>
        <tr>
            <td>Banner-University Medical Center South Campus</td>
            <td>Tucson</td>
            <td>AZ</td>
            <td>7.0</td>
        </tr>
        <tr>
            <td>MultiCare Health System</td>
            <td>None</td>
            <td>WA</td>
            <td>7.0</td>
        </tr>
        <tr>
            <td>Saint Alphonsus Medical Center - Nampa</td>
            <td>Nampa</td>
            <td>ID</td>
            <td>8.0</td>
        </tr>
        <tr>
            <td>University of Vermont Health Network</td>
            <td>None</td>
            <td>NY</td>
            <td>8.0</td>
        </tr>
        <tr>
            <td>Prime Healthcare Services</td>
            <td>None</td>
            <td>IN</td>
            <td>9.0</td>
        </tr>
        <tr>
            <td>Saint Alphonsus Medical Center - Ontario</td>
            <td>Ontario</td>
            <td>OR</td>
            <td>9.0</td>
        </tr>
        <tr>
            <td>Denver Health Medical Center</td>
            <td>Denver</td>
            <td>CO</td>
            <td>10.0</td>
        </tr>
        <tr>
            <td>VCU Health System</td>
            <td>None</td>
            <td>VA</td>
            <td>10.0</td>
        </tr>
        <tr>
            <td>Sharp HealthCare</td>
            <td>None</td>
            <td>CA</td>
            <td>11.0</td>
        </tr>
        <tr>
            <td>St. Rose Dominican Hospitals - Rose De Lima Campus</td>
            <td>Henderson</td>
            <td>NV</td>
            <td>11.0</td>
        </tr>
        <tr>
            <td>Centura Health-St. Mary Corwin Medical Center</td>
            <td>Pueblo</td>
            <td>CO</td>
            <td>12.0</td>
        </tr>
        <tr>
            <td>Palomar Health</td>
            <td>None</td>
            <td>CA</td>
            <td>12.0</td>
        </tr>
        <tr>
            <td>Adena Health System</td>
            <td>None</td>
            <td>OH</td>
            <td>13.0</td>
        </tr>
        <tr>
            <td>Saint Joseph Berea</td>
            <td>Berea</td>
            <td>KY</td>
            <td>13.0</td>
        </tr>
        <tr>
            <td>Memorial Hermann Health System</td>
            <td>None</td>
            <td>TX</td>
            <td>14.0</td>
        </tr>
        <tr>
            <td>St. Charles Prineville</td>
            <td>Prineville</td>
            <td>OR</td>
            <td>14.0</td>
        </tr>
        <tr>
            <td>Lehigh Valley Health Network</td>
            <td>None</td>
            <td>PA</td>
            <td>15.0</td>
        </tr>
        <tr>
            <td>Metrohealth System</td>
            <td>Cleveland</td>
            <td>OH</td>
            <td>15.0</td>
        </tr>
        <tr>
            <td>St. Charles Health System</td>
            <td>None</td>
            <td>OR</td>
            <td>16.0</td>
        </tr>
        <tr>
            <td>Stoughton Hospital</td>
            <td>Stoughton</td>
            <td>WI</td>
            <td>16.0</td>
        </tr>
        <tr>
            <td>Legacy Health</td>
            <td>None</td>
            <td>OR</td>
            <td>17.0</td>
        </tr>
        <tr>
            <td>Sutter Solano Medical Center</td>
            <td>Vallejo</td>
            <td>CA</td>
            <td>17.0</td>
        </tr>
        <tr>
            <td>Essentia Health</td>
            <td>None</td>
            <td>MN</td>
            <td>18.0</td>
        </tr>
        <tr>
            <td>Providence Milwaukie Hospital</td>
            <td>Milwaukie</td>
            <td>OR</td>
            <td>18.0</td>
        </tr>
        <tr>
            <td>North Suburban Medical Center</td>
            <td>Thornton</td>
            <td>CO</td>
            <td>19.0</td>
        </tr>
        <tr>
            <td>SolutioNHealth</td>
            <td>None</td>
            <td>NH</td>
            <td>19.0</td>
        </tr>
        <tr>
            <td>Baystate Wing Hospital and Medical Centers</td>
            <td>Palmer</td>
            <td>MA</td>
            <td>20.0</td>
        </tr>
        <tr>
            <td>Sentara Healthcare</td>
            <td>None</td>
            <td>NC</td>
            <td>20.0</td>
        </tr>
        <tr>
            <td>Medical Center of the Rockies</td>
            <td>Loveland</td>
            <td>CO</td>
            <td>21.0</td>
        </tr>
        <tr>
            <td>UC Health (Cincinnati)</td>
            <td>None</td>
            <td>OH</td>
            <td>21.0</td>
        </tr>
        <tr>
            <td>Atrium Health University City</td>
            <td>Charlotte</td>
            <td>NC</td>
            <td>22.0</td>
        </tr>
        <tr>
            <td>Baylor Scott &amp; White Health</td>
            <td>None</td>
            <td>TX</td>
            <td>22.0</td>
        </tr>
        <tr>
            <td>Lee Memorial Hospital</td>
            <td>Fort Myers</td>
            <td>FL</td>
            <td>23.0</td>
        </tr>
        <tr>
            <td>Penn State Health</td>
            <td>None</td>
            <td>PA</td>
            <td>23.0</td>
        </tr>
        <tr>
            <td>Excela Health Frick Hospital</td>
            <td>Mount Pleasant</td>
            <td>PA</td>
            <td>24.0</td>
        </tr>
        <tr>
            <td>Tristar Stonecrest Medical Center</td>
            <td>Smyrna</td>
            <td>TN</td>
            <td>25.0</td>
        </tr>
        <tr>
            <td>UW Medicine (Washington)</td>
            <td>None</td>
            <td>WA</td>
            <td>25.0</td>
        </tr>
        <tr>
            <td>CentraCare Health System</td>
            <td>None</td>
            <td>MN</td>
            <td>26.0</td>
        </tr>
        <tr>
            <td>Providence St. Joseph Medical Center</td>
            <td>Polson</td>
            <td>MT</td>
            <td>26.0</td>
        </tr>
        <tr>
            <td>Avanti Hospitals</td>
            <td>None</td>
            <td>CA</td>
            <td>27.0</td>
        </tr>
        <tr>
            <td>California Pacific Medical Center - Mission Bernal</td>
            <td>San Francisco</td>
            <td>CA</td>
            <td>27.0</td>
        </tr>
        <tr>
            <td>Centra Health</td>
            <td>None</td>
            <td>VA</td>
            <td>28.0</td>
        </tr>
        <tr>
            <td>Saint Michael&#x27;s Medical Center</td>
            <td>Newark</td>
            <td>NJ</td>
            <td>28.0</td>
        </tr>
        <tr>
            <td>Presbyterian Healthcare Services</td>
            <td>None</td>
            <td>NM</td>
            <td>29.0</td>
        </tr>
        <tr>
            <td>Munson Healthcare Cadillac Hospital</td>
            <td>Cadillac</td>
            <td>MI</td>
            <td>30.0</td>
        </tr>
        <tr>
            <td>Rochester Regional Health System</td>
            <td>None</td>
            <td>NY</td>
            <td>30.0</td>
        </tr>
        <tr>
            <td>Lee Health</td>
            <td>None</td>
            <td>FL</td>
            <td>31.0</td>
        </tr>
        <tr>
            <td>Riverside University Health System-Medical Center</td>
            <td>Moreno Valley</td>
            <td>CA</td>
            <td>31.0</td>
        </tr>
        <tr>
            <td>Garden Grove Hospital &amp; Medical Center</td>
            <td>Garden Grove</td>
            <td>CA</td>
            <td>32.0</td>
        </tr>
        <tr>
            <td>Hawaii Health Systems Corporation</td>
            <td>None</td>
            <td>HI</td>
            <td>32.0</td>
        </tr>
        <tr>
            <td>Asante Health System</td>
            <td>None</td>
            <td>OR</td>
            <td>33.0</td>
        </tr>
        <tr>
            <td>Uintah Basin Medical Center</td>
            <td>Roosevelt</td>
            <td>UT</td>
            <td>33.0</td>
        </tr>
        <tr>
            <td>Hawaii Pacific Health</td>
            <td>None</td>
            <td>HI</td>
            <td>34.0</td>
        </tr>
        <tr>
            <td>Chi Health Immanuel</td>
            <td>Omaha</td>
            <td>NE</td>
            <td>35.0</td>
        </tr>
        <tr>
            <td>University of Pennsylvania Health System</td>
            <td>None</td>
            <td>PA</td>
            <td>35.0</td>
        </tr>
        <tr>
            <td>Allina Health System</td>
            <td>None</td>
            <td>MN</td>
            <td>36.0</td>
        </tr>
        <tr>
            <td>St. Elizabeth Community Hospital</td>
            <td>Red Bluff</td>
            <td>CA</td>
            <td>36.0</td>
        </tr>
        <tr>
            <td>Petaluma Valley Hospital</td>
            <td>Petaluma</td>
            <td>CA</td>
            <td>37.0</td>
        </tr>
        <tr>
            <td>Saint Lukes Hospital of Duluth</td>
            <td>None</td>
            <td>MN</td>
            <td>37.0</td>
        </tr>
        <tr>
            <td>Research Medical Center</td>
            <td>Kansas City</td>
            <td>MO</td>
            <td>38.0</td>
        </tr>
        <tr>
            <td>University of California Health</td>
            <td>None</td>
            <td>CA</td>
            <td>38.0</td>
        </tr>
        <tr>
            <td>Alliance Community Hospital</td>
            <td>Alliance</td>
            <td>OH</td>
            <td>39.0</td>
        </tr>
        <tr>
            <td>HealthPartners</td>
            <td>None</td>
            <td>MN</td>
            <td>39.0</td>
        </tr>
        <tr>
            <td>Tristar Southern Hills Medical Center</td>
            <td>Nashville</td>
            <td>TN</td>
            <td>40.0</td>
        </tr>
        <tr>
            <td>Duke University Health System</td>
            <td>None</td>
            <td>NC</td>
            <td>41.0</td>
        </tr>
        <tr>
            <td>Spotsylvania Regional Medical Center</td>
            <td>Fredericksburg</td>
            <td>VA</td>
            <td>41.0</td>
        </tr>
        <tr>
            <td>Barton Health</td>
            <td>None</td>
            <td>CA</td>
            <td>42.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Hospital - Monroe Campus</td>
            <td>Stroudsburg</td>
            <td>PA</td>
            <td>42.0</td>
        </tr>
        <tr>
            <td>Beth Israel Lahey Health</td>
            <td>None</td>
            <td>MA</td>
            <td>43.0</td>
        </tr>
        <tr>
            <td>Gouverneur Hospital</td>
            <td>Gouverneur</td>
            <td>NY</td>
            <td>43.0</td>
        </tr>
        <tr>
            <td>Landmark Medical Center</td>
            <td>Woonsocket</td>
            <td>RI</td>
            <td>44.0</td>
        </tr>
        <tr>
            <td>SCL Health</td>
            <td>None</td>
            <td>CO</td>
            <td>44.0</td>
        </tr>
        <tr>
            <td>St. Charles Redmond</td>
            <td>Redmond</td>
            <td>OR</td>
            <td>45.0</td>
        </tr>
        <tr>
            <td>University of Kansas Health System</td>
            <td>None</td>
            <td>KS</td>
            <td>45.0</td>
        </tr>
        <tr>
            <td>Alaska Regional Hospital</td>
            <td>Anchorage</td>
            <td>AK</td>
            <td>46.0</td>
        </tr>
        <tr>
            <td>Johns Hopkins Health System</td>
            <td>None</td>
            <td>DC</td>
            <td>46.0</td>
        </tr>
        <tr>
            <td>St. Anthony Hospital</td>
            <td>Pendleton</td>
            <td>OR</td>
            <td>47.0</td>
        </tr>
        <tr>
            <td>Wakemed Health and Hospitals</td>
            <td>None</td>
            <td>NC</td>
            <td>47.0</td>
        </tr>
        <tr>
            <td>M Health Fairview</td>
            <td>None</td>
            <td>MN</td>
            <td>48.0</td>
        </tr>
        <tr>
            <td>Sharp Chula Vista Medical Center</td>
            <td>Chula Vista</td>
            <td>CA</td>
            <td>48.0</td>
        </tr>
        <tr>
            <td>Lawrence General Hospital</td>
            <td>Lawrence</td>
            <td>MA</td>
            <td>49.0</td>
        </tr>
        <tr>
            <td>Rush University Health</td>
            <td>None</td>
            <td>IL</td>
            <td>49.0</td>
        </tr>
        <tr>
            <td>Dallas Regional Medical Center</td>
            <td>Mesquite</td>
            <td>TX</td>
            <td>50.0</td>
        </tr>
        <tr>
            <td>Excela Health</td>
            <td>None</td>
            <td>PA</td>
            <td>50.0</td>
        </tr>
        <tr>
            <td>Promedica Bixby Hospital</td>
            <td>Adrian</td>
            <td>MI</td>
            <td>51.0</td>
        </tr>
        <tr>
            <td>WellSpan Health</td>
            <td>None</td>
            <td>PA</td>
            <td>51.0</td>
        </tr>
        <tr>
            <td>Providence</td>
            <td>None</td>
            <td>MT</td>
            <td>52.0</td>
        </tr>
        <tr>
            <td>Wakemed Raleigh Campus</td>
            <td>Raleigh</td>
            <td>NC</td>
            <td>52.0</td>
        </tr>
        <tr>
            <td>Multicare Auburn Medical Center</td>
            <td>Auburn</td>
            <td>WA</td>
            <td>53.0</td>
        </tr>
        <tr>
            <td>Munson Healthcare</td>
            <td>None</td>
            <td>MI</td>
            <td>53.0</td>
        </tr>
        <tr>
            <td>Beth Israel Deaconess Hospital - Plymouth</td>
            <td>Plymouth</td>
            <td>MA</td>
            <td>54.0</td>
        </tr>
        <tr>
            <td>Cone Health</td>
            <td>None</td>
            <td>NC</td>
            <td>54.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>KY</td>
            <td>55.0</td>
        </tr>
        <tr>
            <td>Paradise Valley Hospital</td>
            <td>National City</td>
            <td>CA</td>
            <td>55.0</td>
        </tr>
        <tr>
            <td>SSM Health St. Mary&#x27;s Hospital - St. Louis</td>
            <td>Richmond Heights</td>
            <td>MO</td>
            <td>56.0</td>
        </tr>
        <tr>
            <td>Yale New Haven Health System</td>
            <td>None</td>
            <td>CT</td>
            <td>56.0</td>
        </tr>
        <tr>
            <td>Angel Medical Center</td>
            <td>Franklin</td>
            <td>NC</td>
            <td>57.0</td>
        </tr>
        <tr>
            <td>Bon Secours Mercy Health System</td>
            <td>None</td>
            <td>OH</td>
            <td>57.0</td>
        </tr>
        <tr>
            <td>Banner Health</td>
            <td>None</td>
            <td>CO</td>
            <td>58.0</td>
        </tr>
        <tr>
            <td>JPS Health Network</td>
            <td>Fort Worth</td>
            <td>TX</td>
            <td>58.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>KS</td>
            <td>59.0</td>
        </tr>
        <tr>
            <td>Peninsula Regional Medical Center</td>
            <td>Salisbury</td>
            <td>MD</td>
            <td>59.0</td>
        </tr>
        <tr>
            <td>New York Presbyterian</td>
            <td>None</td>
            <td>NY</td>
            <td>60.0</td>
        </tr>
        <tr>
            <td>Parkland Health Center</td>
            <td>Farmington</td>
            <td>MO</td>
            <td>60.0</td>
        </tr>
        <tr>
            <td>Froedtert and The Medical College of Wisconsin</td>
            <td>None</td>
            <td>WI</td>
            <td>61.0</td>
        </tr>
        <tr>
            <td>Providence Holy Cross Medical Center</td>
            <td>Mission Hills</td>
            <td>CA</td>
            <td>61.0</td>
        </tr>
        <tr>
            <td>Mount Sinai Health System</td>
            <td>None</td>
            <td>NY</td>
            <td>62.0</td>
        </tr>
        <tr>
            <td>St. Bernardine Medical Center</td>
            <td>San Bernardino</td>
            <td>CA</td>
            <td>62.0</td>
        </tr>
        <tr>
            <td>Hartford Healthcare</td>
            <td>None</td>
            <td>CT</td>
            <td>63.0</td>
        </tr>
        <tr>
            <td>St. Mary&#x27;s General Hospital</td>
            <td>Passaic</td>
            <td>NJ</td>
            <td>63.0</td>
        </tr>
        <tr>
            <td>Ascension Healthcare</td>
            <td>None</td>
            <td>IN</td>
            <td>64.0</td>
        </tr>
        <tr>
            <td>John Randolph Medical Center</td>
            <td>Hopewell</td>
            <td>VA</td>
            <td>64.0</td>
        </tr>
        <tr>
            <td>UVA Health System</td>
            <td>None</td>
            <td>VA</td>
            <td>65.0</td>
        </tr>
        <tr>
            <td>UofLÂ¬â€ Health - Jewish Hospital</td>
            <td>Louisville</td>
            <td>KY</td>
            <td>65.0</td>
        </tr>
        <tr>
            <td>Northwell Health</td>
            <td>None</td>
            <td>NY</td>
            <td>66.0</td>
        </tr>
        <tr>
            <td>Samaritan Hospital</td>
            <td>Troy</td>
            <td>NY</td>
            <td>66.0</td>
        </tr>
        <tr>
            <td>St. Anthony Summit Medical Center</td>
            <td>Frisco</td>
            <td>CO</td>
            <td>67.0</td>
        </tr>
        <tr>
            <td>University of Maryland Medical System</td>
            <td>None</td>
            <td>MD</td>
            <td>67.0</td>
        </tr>
        <tr>
            <td>Carilion Giles Community Hospital</td>
            <td>Pearisburg</td>
            <td>VA</td>
            <td>68.0</td>
        </tr>
        <tr>
            <td>Vanderbilt Health</td>
            <td>None</td>
            <td>TN</td>
            <td>68.0</td>
        </tr>
        <tr>
            <td>Poudre Valley Hospital</td>
            <td>Fort Collins</td>
            <td>CO</td>
            <td>69.0</td>
        </tr>
        <tr>
            <td>Renown Health</td>
            <td>None</td>
            <td>NV</td>
            <td>69.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System - Fairmont</td>
            <td>Fairmont</td>
            <td>MN</td>
            <td>70.0</td>
        </tr>
        <tr>
            <td>MercyOne</td>
            <td>None</td>
            <td>IA</td>
            <td>70.0</td>
        </tr>
        <tr>
            <td>Beaumont Health Systems</td>
            <td>None</td>
            <td>MI</td>
            <td>71.0</td>
        </tr>
        <tr>
            <td>Penn Presbyterian Medical Center</td>
            <td>Philadelphia</td>
            <td>PA</td>
            <td>71.0</td>
        </tr>
        <tr>
            <td>Cleveland Clinic Health System</td>
            <td>None</td>
            <td>FL</td>
            <td>72.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System in Red Wing</td>
            <td>Red Wing</td>
            <td>MN</td>
            <td>72.0</td>
        </tr>
        <tr>
            <td>Baylor Scott &amp; White Clinic - Temple</td>
            <td>Temple</td>
            <td>TX</td>
            <td>73.0</td>
        </tr>
        <tr>
            <td>Parkview Health System</td>
            <td>None</td>
            <td>IN</td>
            <td>73.0</td>
        </tr>
        <tr>
            <td>Aspirus</td>
            <td>None</td>
            <td>MI</td>
            <td>74.0</td>
        </tr>
        <tr>
            <td>Providence Mount Carmel Hospital</td>
            <td>Colville</td>
            <td>WA</td>
            <td>74.0</td>
        </tr>
        <tr>
            <td>Prisma Health</td>
            <td>None</td>
            <td>SC</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Hospital Bethlehem</td>
            <td>Bethlehem</td>
            <td>PA</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Christiana Care Health System</td>
            <td>None</td>
            <td>DE</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Providence Newberg Medical Center</td>
            <td>Newberg</td>
            <td>OR</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Central Maine Healthcare</td>
            <td>None</td>
            <td>ME</td>
            <td>77.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System - Mankato</td>
            <td>Mankato</td>
            <td>MN</td>
            <td>77.0</td>
        </tr>
        <tr>
            <td>California Pacific Medical Center- Van Ness Campus</td>
            <td>San Francisco</td>
            <td>CA</td>
            <td>78.0</td>
        </tr>
        <tr>
            <td>Lifespan</td>
            <td>None</td>
            <td>RI</td>
            <td>78.0</td>
        </tr>
        <tr>
            <td>PeaceHealth</td>
            <td>None</td>
            <td>AK</td>
            <td>79.0</td>
        </tr>
        <tr>
            <td>Carle Health</td>
            <td>None</td>
            <td>IL</td>
            <td>80.0</td>
        </tr>
        <tr>
            <td>Providence Portland Medical Center</td>
            <td>Portland</td>
            <td>OR</td>
            <td>80.0</td>
        </tr>
        <tr>
            <td>Sparrow Health System</td>
            <td>None</td>
            <td>MI</td>
            <td>81.0</td>
        </tr>
        <tr>
            <td>University of Maryland Medical Center Midtown Campus</td>
            <td>Baltimore</td>
            <td>MD</td>
            <td>81.0</td>
        </tr>
        <tr>
            <td>Adventist Health</td>
            <td>None</td>
            <td>CA</td>
            <td>82.0</td>
        </tr>
        <tr>
            <td>Inova Loudoun Hospital</td>
            <td>Leesburg</td>
            <td>VA</td>
            <td>82.0</td>
        </tr>
        <tr>
            <td>University of Chicago Medicine</td>
            <td>None</td>
            <td>IL</td>
            <td>83.0</td>
        </tr>
        <tr>
            <td>West Valley Medical Center</td>
            <td>Caldwell</td>
            <td>ID</td>
            <td>83.0</td>
        </tr>
        <tr>
            <td>Emory University Hospital Midtown</td>
            <td>Atlanta</td>
            <td>GA</td>
            <td>84.0</td>
        </tr>
        <tr>
            <td>Loma Linda University Adventist Health Sciences Center</td>
            <td>None</td>
            <td>CA</td>
            <td>84.0</td>
        </tr>
        <tr>
            <td>Mary Washington Healthcare</td>
            <td>None</td>
            <td>VA</td>
            <td>85.0</td>
        </tr>
        <tr>
            <td>St. David&#x27;s South Austin Medical Center</td>
            <td>Austin</td>
            <td>TX</td>
            <td>85.0</td>
        </tr>
        <tr>
            <td>Berkshire Health Systems</td>
            <td>None</td>
            <td>MA</td>
            <td>86.0</td>
        </tr>
        <tr>
            <td>Southern Maine Health Care</td>
            <td>Biddeford</td>
            <td>ME</td>
            <td>86.0</td>
        </tr>
        <tr>
            <td>Heywood Healthcare</td>
            <td>None</td>
            <td>MA</td>
            <td>87.0</td>
        </tr>
        <tr>
            <td>Providence Willamette Falls Medical Center</td>
            <td>Oregon City</td>
            <td>OR</td>
            <td>87.0</td>
        </tr>
        <tr>
            <td>SSM Health</td>
            <td>None</td>
            <td>MO</td>
            <td>88.0</td>
        </tr>
        <tr>
            <td>St. James Healthcare</td>
            <td>Butte</td>
            <td>MT</td>
            <td>88.0</td>
        </tr>
        <tr>
            <td>Essentia Health St. Mary&#x27;s Medical Center</td>
            <td>Duluth</td>
            <td>MN</td>
            <td>89.0</td>
        </tr>
        <tr>
            <td>Tufts Medicine</td>
            <td>None</td>
            <td>MA</td>
            <td>89.0</td>
        </tr>
        <tr>
            <td>Park Plaza Hospital</td>
            <td>Houston</td>
            <td>TX</td>
            <td>90.0</td>
        </tr>
        <tr>
            <td>Sinai Chicago</td>
            <td>None</td>
            <td>IL</td>
            <td>90.0</td>
        </tr>
        <tr>
            <td>East Liverpool City Hospital</td>
            <td>East Liverpool</td>
            <td>OH</td>
            <td>91.0</td>
        </tr>
        <tr>
            <td>UMass Memorial Health Care</td>
            <td>None</td>
            <td>MA</td>
            <td>91.0</td>
        </tr>
        <tr>
            <td>Inova Health System</td>
            <td>None</td>
            <td>VA</td>
            <td>92.0</td>
        </tr>
        <tr>
            <td>LDS Hospital</td>
            <td>Salt Lake City</td>
            <td>UT</td>
            <td>92.0</td>
        </tr>
        <tr>
            <td>North Colorado Medical Center</td>
            <td>Greeley</td>
            <td>CO</td>
            <td>93.0</td>
        </tr>
        <tr>
            <td>Valley Health System</td>
            <td>None</td>
            <td>VA</td>
            <td>93.0</td>
        </tr>
        <tr>
            <td>SSM Health St. Clare Hospital - Baraboo</td>
            <td>Baraboo</td>
            <td>WI</td>
            <td>94.0</td>
        </tr>
        <tr>
            <td>Scripps Health</td>
            <td>None</td>
            <td>CA</td>
            <td>94.0</td>
        </tr>
        <tr>
            <td>Mid-Columbia Medical Center</td>
            <td>The Dalles</td>
            <td>OR</td>
            <td>95.0</td>
        </tr>
        <tr>
            <td>ProMedica Health System</td>
            <td>None</td>
            <td>MI</td>
            <td>95.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System - Albert Lea and Austin</td>
            <td>Albert Lea</td>
            <td>MN</td>
            <td>96.0</td>
        </tr>
        <tr>
            <td>OhioHealth</td>
            <td>None</td>
            <td>OH</td>
            <td>96.0</td>
        </tr>
        <tr>
            <td>Baptist Health Care</td>
            <td>None</td>
            <td>FL</td>
            <td>97.0</td>
        </tr>
        <tr>
            <td>Legacy Salmon Creek Medical Center</td>
            <td>Vancouver</td>
            <td>WA</td>
            <td>97.0</td>
        </tr>
        <tr>
            <td>Centinela Hospital Medical Center</td>
            <td>Inglewood</td>
            <td>CA</td>
            <td>98.0</td>
        </tr>
        <tr>
            <td>Luminis Health</td>
            <td>None</td>
            <td>MD</td>
            <td>98.0</td>
        </tr>
        <tr>
            <td>The Medical Center of Aurora</td>
            <td>Aurora</td>
            <td>CO</td>
            <td>99.0</td>
        </tr>
        <tr>
            <td>Mercy Health</td>
            <td>None</td>
            <td>KY</td>
            <td>100.0</td>
        </tr>
        <tr>
            <td>University of Colorado Hospital Authority</td>
            <td>Aurora</td>
            <td>CO</td>
            <td>100.0</td>
        </tr>
        <tr>
            <td>Fairview Northland Regional Hospital</td>
            <td>Princeton</td>
            <td>MN</td>
            <td>101.0</td>
        </tr>
        <tr>
            <td>MaineHealth</td>
            <td>None</td>
            <td>ME</td>
            <td>101.0</td>
        </tr>
        <tr>
            <td>TriHealth</td>
            <td>None</td>
            <td>OH</td>
            <td>102.0</td>
        </tr>
        <tr>
            <td>VCU Medical Center</td>
            <td>Richmond</td>
            <td>VA</td>
            <td>102.0</td>
        </tr>
        <tr>
            <td>Hendrick Health System</td>
            <td>None</td>
            <td>TX</td>
            <td>103.0</td>
        </tr>
        <tr>
            <td>St. Patrick Hospital</td>
            <td>Missoula</td>
            <td>MT</td>
            <td>103.0</td>
        </tr>
        <tr>
            <td>Advocate Aurora Health</td>
            <td>None</td>
            <td>IL</td>
            <td>104.0</td>
        </tr>
        <tr>
            <td>Tristar Hendersonville Medical Center</td>
            <td>Hendersonville</td>
            <td>TN</td>
            <td>104.0</td>
        </tr>
        <tr>
            <td>UPMC</td>
            <td>None</td>
            <td>MD</td>
            <td>105.0</td>
        </tr>
        <tr>
            <td>BJC Healthcare</td>
            <td>None</td>
            <td>IL</td>
            <td>106.0</td>
        </tr>
        <tr>
            <td>University of California Davis Medical Center</td>
            <td>Sacramento</td>
            <td>CA</td>
            <td>106.0</td>
        </tr>
        <tr>
            <td>Saint Joseph Mercy Livingston Hospital</td>
            <td>Howell</td>
            <td>MI</td>
            <td>107.0</td>
        </tr>
        <tr>
            <td>Saint Luke&#x27;s Health System</td>
            <td>None</td>
            <td>KS</td>
            <td>107.0</td>
        </tr>
        <tr>
            <td>MemorialCare</td>
            <td>None</td>
            <td>CA</td>
            <td>108.0</td>
        </tr>
        <tr>
            <td>Methodist Dallas Medical Center</td>
            <td>Dallas</td>
            <td>TX</td>
            <td>108.0</td>
        </tr>
        <tr>
            <td>Adventist Health Portland</td>
            <td>Portland</td>
            <td>OR</td>
            <td>109.0</td>
        </tr>
        <tr>
            <td>Orlando Health</td>
            <td>None</td>
            <td>FL</td>
            <td>109.0</td>
        </tr>
        <tr>
            <td>Forks Community Hospital</td>
            <td>Forks</td>
            <td>WA</td>
            <td>110.0</td>
        </tr>
        <tr>
            <td>HonorHealth</td>
            <td>None</td>
            <td>AZ</td>
            <td>110.0</td>
        </tr>
        <tr>
            <td>Ascension Seton Hays</td>
            <td>Kyle</td>
            <td>TX</td>
            <td>111.0</td>
        </tr>
        <tr>
            <td>Washington Health System</td>
            <td>None</td>
            <td>PA</td>
            <td>111.0</td>
        </tr>
        <tr>
            <td>Presbyterian St. Luke&#x27;s Medical Center</td>
            <td>Denver</td>
            <td>CO</td>
            <td>112.0</td>
        </tr>
        <tr>
            <td>Virtua Health</td>
            <td>None</td>
            <td>NJ</td>
            <td>112.0</td>
        </tr>
        <tr>
            <td>Chippewa County Hospital</td>
            <td>Montevideo</td>
            <td>MN</td>
            <td>113.0</td>
        </tr>
        <tr>
            <td>ThedaCare</td>
            <td>None</td>
            <td>WI</td>
            <td>113.0</td>
        </tr>
        <tr>
            <td>St. Lukes Hospital</td>
            <td>Cedar Rapids</td>
            <td>IA</td>
            <td>114.0</td>
        </tr>
        <tr>
            <td>Cottage Health System</td>
            <td>None</td>
            <td>CA</td>
            <td>115.0</td>
        </tr>
        <tr>
            <td>Rush University Medical Center</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>115.0</td>
        </tr>
        <tr>
            <td>Mass General Brigham</td>
            <td>None</td>
            <td>MA</td>
            <td>116.0</td>
        </tr>
        <tr>
            <td>Piedmont Athens Regional Medical Center</td>
            <td>Athens</td>
            <td>GA</td>
            <td>116.0</td>
        </tr>
        <tr>
            <td>Community Memorial Health System</td>
            <td>None</td>
            <td>CA</td>
            <td>117.0</td>
        </tr>
        <tr>
            <td>Sentara Careplex Hospital</td>
            <td>Hampton</td>
            <td>VA</td>
            <td>117.0</td>
        </tr>
        <tr>
            <td>Firsthealth of The Carolinas</td>
            <td>None</td>
            <td>NC</td>
            <td>118.0</td>
        </tr>
        <tr>
            <td>Legacy Good Samaritan Medical Center</td>
            <td>Portland</td>
            <td>OR</td>
            <td>118.0</td>
        </tr>
        <tr>
            <td>CHI St. Josephâ€šÃ„Ã´s Health of Park Rapids</td>
            <td>Park Rapids</td>
            <td>MN</td>
            <td>119.0</td>
        </tr>
        <tr>
            <td>Northwestern Memorial Medicine</td>
            <td>None</td>
            <td>IL</td>
            <td>119.0</td>
        </tr>
        <tr>
            <td>Fairview Park Hospital</td>
            <td>Dublin</td>
            <td>GA</td>
            <td>120.0</td>
        </tr>
        <tr>
            <td>John Muir Health</td>
            <td>None</td>
            <td>CA</td>
            <td>120.0</td>
        </tr>
        <tr>
            <td>Bellevue Medical Center</td>
            <td>Bellevue</td>
            <td>NE</td>
            <td>121.0</td>
        </tr>
        <tr>
            <td>Riverside Health System</td>
            <td>None</td>
            <td>VA</td>
            <td>121.0</td>
        </tr>
        <tr>
            <td>Asante Rogue Regional Medical Center</td>
            <td>Medford</td>
            <td>OR</td>
            <td>122.0</td>
        </tr>
        <tr>
            <td>Atlantic Health System</td>
            <td>None</td>
            <td>NJ</td>
            <td>122.0</td>
        </tr>
        <tr>
            <td>NorthShore University Health System</td>
            <td>None</td>
            <td>IL</td>
            <td>123.0</td>
        </tr>
        <tr>
            <td>St. Charles Medical Center - Bend</td>
            <td>Bend</td>
            <td>OR</td>
            <td>123.0</td>
        </tr>
        <tr>
            <td>UW Health (Wisconsin)</td>
            <td>None</td>
            <td>IL</td>
            <td>124.0</td>
        </tr>
        <tr>
            <td>Main Line Health</td>
            <td>None</td>
            <td>PA</td>
            <td>125.0</td>
        </tr>
        <tr>
            <td>Mission Community Hospital</td>
            <td>Panorama City</td>
            <td>CA</td>
            <td>125.0</td>
        </tr>
        <tr>
            <td>Dell SetonÂ¬â€  Medical Center at the University of Texas</td>
            <td>Austin</td>
            <td>TX</td>
            <td>126.0</td>
        </tr>
        <tr>
            <td>ProHealth Care</td>
            <td>None</td>
            <td>WI</td>
            <td>126.0</td>
        </tr>
        <tr>
            <td>Benefis Hospitals</td>
            <td>Great Falls</td>
            <td>MT</td>
            <td>127.0</td>
        </tr>
        <tr>
            <td>Emory Healthcare</td>
            <td>None</td>
            <td>GA</td>
            <td>127.0</td>
        </tr>
        <tr>
            <td>St. Joseph Regional Health Center</td>
            <td>Bryan</td>
            <td>TX</td>
            <td>128.0</td>
        </tr>
        <tr>
            <td>University of Rochester Medical Center</td>
            <td>None</td>
            <td>NY</td>
            <td>128.0</td>
        </tr>
        <tr>
            <td>Nuvance Health</td>
            <td>None</td>
            <td>CT</td>
            <td>129.0</td>
        </tr>
        <tr>
            <td>Inova Alexandria Hospital</td>
            <td>Alexandria</td>
            <td>VA</td>
            <td>130.0</td>
        </tr>
        <tr>
            <td>Sanford Health</td>
            <td>None</td>
            <td>MN</td>
            <td>130.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Health System</td>
            <td>None</td>
            <td>ID</td>
            <td>131.0</td>
        </tr>
        <tr>
            <td>UCHealth Memorial Hospital Central</td>
            <td>Colorado Springs</td>
            <td>CO</td>
            <td>131.0</td>
        </tr>
        <tr>
            <td>Covenant Health Systems</td>
            <td>None</td>
            <td>ME</td>
            <td>132.0</td>
        </tr>
        <tr>
            <td>St. Clare Hospital</td>
            <td>Lakewood</td>
            <td>WA</td>
            <td>132.0</td>
        </tr>
        <tr>
            <td>MedStar Health</td>
            <td>None</td>
            <td>DC</td>
            <td>133.0</td>
        </tr>
        <tr>
            <td>University Health System</td>
            <td>San Antonio</td>
            <td>TX</td>
            <td>133.0</td>
        </tr>
        <tr>
            <td>WellStar Health System</td>
            <td>None</td>
            <td>GA</td>
            <td>134.0</td>
        </tr>
        <tr>
            <td>Adventist Healthcare</td>
            <td>None</td>
            <td>MD</td>
            <td>135.0</td>
        </tr>
        <tr>
            <td>Buffalo Hospital</td>
            <td>Buffalo</td>
            <td>MN</td>
            <td>135.0</td>
        </tr>
        <tr>
            <td>Beth Israel Deaconess Hospital-Milton</td>
            <td>Milton</td>
            <td>MA</td>
            <td>136.0</td>
        </tr>
        <tr>
            <td>Garnet Health</td>
            <td>None</td>
            <td>NY</td>
            <td>136.0</td>
        </tr>
        <tr>
            <td>Bronson Healthcare</td>
            <td>None</td>
            <td>MI</td>
            <td>137.0</td>
        </tr>
        <tr>
            <td>Skyline Hospital</td>
            <td>White Salmon</td>
            <td>WA</td>
            <td>137.0</td>
        </tr>
        <tr>
            <td>Baylor University Medical Center</td>
            <td>Dallas</td>
            <td>TX</td>
            <td>138.0</td>
        </tr>
        <tr>
            <td>Concord Hospital Health System</td>
            <td>None</td>
            <td>NH</td>
            <td>138.0</td>
        </tr>
        <tr>
            <td>Monadnock Community Hospital</td>
            <td>Peterborough</td>
            <td>NH</td>
            <td>139.0</td>
        </tr>
        <tr>
            <td>Northern Arizona Healthcare</td>
            <td>None</td>
            <td>AZ</td>
            <td>139.0</td>
        </tr>
        <tr>
            <td>Capital Health System</td>
            <td>None</td>
            <td>NJ</td>
            <td>140.0</td>
        </tr>
        <tr>
            <td>Montrose Memorial Hospital</td>
            <td>Montrose</td>
            <td>CO</td>
            <td>141.0</td>
        </tr>
        <tr>
            <td>Saint Francis Health System</td>
            <td>None</td>
            <td>OK</td>
            <td>141.0</td>
        </tr>
        <tr>
            <td>Milton S. Hershey Medical Center</td>
            <td>Hershey</td>
            <td>PA</td>
            <td>142.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>IA</td>
            <td>142.0</td>
        </tr>
        <tr>
            <td>Christian Hospital Northeast-Northwest</td>
            <td>Saint Louis</td>
            <td>MO</td>
            <td>143.0</td>
        </tr>
        <tr>
            <td>Prospect Medical Holdings</td>
            <td>None</td>
            <td>CT</td>
            <td>143.0</td>
        </tr>
        <tr>
            <td>Carilion Clinic</td>
            <td>None</td>
            <td>VA</td>
            <td>144.0</td>
        </tr>
        <tr>
            <td>Wahiawa General Hospital</td>
            <td>Wahiawa</td>
            <td>HI</td>
            <td>144.0</td>
        </tr>
        <tr>
            <td>Deaconess Health System</td>
            <td>None</td>
            <td>IN</td>
            <td>145.0</td>
        </tr>
        <tr>
            <td>Sanford Worthington Medical Center</td>
            <td>Worthington</td>
            <td>MN</td>
            <td>145.0</td>
        </tr>
        <tr>
            <td>Inspira Health Network</td>
            <td>None</td>
            <td>NJ</td>
            <td>146.0</td>
        </tr>
        <tr>
            <td>Saint Alphonsus Regional Medical Center</td>
            <td>Boise</td>
            <td>ID</td>
            <td>146.0</td>
        </tr>
        <tr>
            <td>Grand River Medical Center</td>
            <td>Rifle</td>
            <td>CO</td>
            <td>147.0</td>
        </tr>
        <tr>
            <td>Unitypoint Health</td>
            <td>None</td>
            <td>IL</td>
            <td>147.0</td>
        </tr>
        <tr>
            <td>Saint Josephs Candler Health System</td>
            <td>None</td>
            <td>GA</td>
            <td>148.0</td>
        </tr>
        <tr>
            <td>Wellstar Paulding Hospital</td>
            <td>Hiram</td>
            <td>GA</td>
            <td>148.0</td>
        </tr>
        <tr>
            <td>Atrium Health</td>
            <td>None</td>
            <td>GA</td>
            <td>149.0</td>
        </tr>
        <tr>
            <td>Cedar City Hospital</td>
            <td>Cedar City</td>
            <td>UT</td>
            <td>149.0</td>
        </tr>
        <tr>
            <td>Beacon Health System</td>
            <td>None</td>
            <td>IN</td>
            <td>150.0</td>
        </tr>
        <tr>
            <td>Highline Medical Center</td>
            <td>Burien</td>
            <td>WA</td>
            <td>150.0</td>
        </tr>
        <tr>
            <td>Cayuga Medical Center</td>
            <td>None</td>
            <td>NY</td>
            <td>151.0</td>
        </tr>
        <tr>
            <td>Santa Barbara Cottage Hospital</td>
            <td>Santa Barbara</td>
            <td>CA</td>
            <td>151.0</td>
        </tr>
        <tr>
            <td>Carepoint Health</td>
            <td>None</td>
            <td>NJ</td>
            <td>152.0</td>
        </tr>
        <tr>
            <td>Lovelace Westside Hospital</td>
            <td>Albuquerque</td>
            <td>NM</td>
            <td>152.0</td>
        </tr>
        <tr>
            <td>Methodist Health System</td>
            <td>None</td>
            <td>TX</td>
            <td>153.0</td>
        </tr>
        <tr>
            <td>St. David&#x27;s Medical Center</td>
            <td>Austin</td>
            <td>TX</td>
            <td>153.0</td>
        </tr>
        <tr>
            <td>Eden Medical Center</td>
            <td>Castro Valley</td>
            <td>CA</td>
            <td>154.0</td>
        </tr>
        <tr>
            <td>University Health Care System</td>
            <td>None</td>
            <td>GA</td>
            <td>154.0</td>
        </tr>
        <tr>
            <td>RWJBarnabas Health</td>
            <td>None</td>
            <td>NJ</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>Multicare Good Samaritan Hospital</td>
            <td>Puyallup</td>
            <td>WA</td>
            <td>156.0</td>
        </tr>
        <tr>
            <td>OSF Healthcare System</td>
            <td>None</td>
            <td>IL</td>
            <td>156.0</td>
        </tr>
        <tr>
            <td>Ballad Health</td>
            <td>None</td>
            <td>TN</td>
            <td>157.0</td>
        </tr>
        <tr>
            <td>Griffin Hospital</td>
            <td>Derby</td>
            <td>CT</td>
            <td>157.0</td>
        </tr>
        <tr>
            <td>Universal Health Services</td>
            <td>None</td>
            <td>FL</td>
            <td>158.0</td>
        </tr>
        <tr>
            <td>Franciscan Sisters of Christian Charity Sponsored Ministries, Inc.</td>
            <td>None</td>
            <td>NE</td>
            <td>159.0</td>
        </tr>
        <tr>
            <td>Longmont United Hospital</td>
            <td>Longmont</td>
            <td>CO</td>
            <td>159.0</td>
        </tr>
        <tr>
            <td>Mckee Medical Center</td>
            <td>Loveland</td>
            <td>CO</td>
            <td>160.0</td>
        </tr>
        <tr>
            <td>Truman Medical Centers</td>
            <td>None</td>
            <td>MO</td>
            <td>160.0</td>
        </tr>
        <tr>
            <td>Einstein Healthcare Network</td>
            <td>None</td>
            <td>PA</td>
            <td>161.0</td>
        </tr>
        <tr>
            <td>Sky Lakes Medical Center</td>
            <td>Klamath Falls</td>
            <td>OR</td>
            <td>161.0</td>
        </tr>
        <tr>
            <td>Baystate Health</td>
            <td>None</td>
            <td>MA</td>
            <td>162.0</td>
        </tr>
        <tr>
            <td>Piedmont Healthcare</td>
            <td>None</td>
            <td>GA</td>
            <td>163.0</td>
        </tr>
        <tr>
            <td>Sentara Obici Hospital</td>
            <td>Suffolk</td>
            <td>VA</td>
            <td>163.0</td>
        </tr>
        <tr>
            <td>Inova Fair Oaks Hospital</td>
            <td>Fairfax</td>
            <td>VA</td>
            <td>164.0</td>
        </tr>
        <tr>
            <td>University Hospitals</td>
            <td>None</td>
            <td>OH</td>
            <td>164.0</td>
        </tr>
        <tr>
            <td>Health First</td>
            <td>None</td>
            <td>FL</td>
            <td>165.0</td>
        </tr>
        <tr>
            <td>Swedish Edmonds Hospital</td>
            <td>Edmonds</td>
            <td>WA</td>
            <td>165.0</td>
        </tr>
        <tr>
            <td>AdventHealth</td>
            <td>None</td>
            <td>GA</td>
            <td>166.0</td>
        </tr>
        <tr>
            <td>Ascension Seton Williamson</td>
            <td>Round Rock</td>
            <td>TX</td>
            <td>166.0</td>
        </tr>
        <tr>
            <td>Allegheny Health Network</td>
            <td>None</td>
            <td>PA</td>
            <td>167.0</td>
        </tr>
        <tr>
            <td>McPherson Hospital</td>
            <td>McPherson</td>
            <td>KS</td>
            <td>167.0</td>
        </tr>
        <tr>
            <td>Asante Three Rivers Medical Center</td>
            <td>Grants Pass</td>
            <td>OR</td>
            <td>168.0</td>
        </tr>
        <tr>
            <td>Seton Medical Center Austin</td>
            <td>Austin</td>
            <td>TX</td>
            <td>169.0</td>
        </tr>
        <tr>
            <td>Texas Health Resources</td>
            <td>None</td>
            <td>TX</td>
            <td>169.0</td>
        </tr>
        <tr>
            <td>Bryan Health</td>
            <td>None</td>
            <td>NE</td>
            <td>170.0</td>
        </tr>
        <tr>
            <td>Penobscot Bay Medical Center</td>
            <td>Rockport</td>
            <td>ME</td>
            <td>171.0</td>
        </tr>
        <tr>
            <td>Hackensack Meridian Health</td>
            <td>None</td>
            <td>NJ</td>
            <td>172.0</td>
        </tr>
        <tr>
            <td>St. Vincent Healthcare</td>
            <td>Billings</td>
            <td>MT</td>
            <td>172.0</td>
        </tr>
        <tr>
            <td>Seton Northwest Hospital</td>
            <td>Austin</td>
            <td>TX</td>
            <td>173.0</td>
        </tr>
        <tr>
            <td>Stillwater Medical Center Authority</td>
            <td>None</td>
            <td>OK</td>
            <td>173.0</td>
        </tr>
        <tr>
            <td>Kettering Health Network</td>
            <td>None</td>
            <td>OH</td>
            <td>174.0</td>
        </tr>
        <tr>
            <td>Page Memorial Hospital</td>
            <td>Luray</td>
            <td>VA</td>
            <td>174.0</td>
        </tr>
        <tr>
            <td>Avera Marshall Regional Medical Ctr</td>
            <td>Marshall</td>
            <td>MN</td>
            <td>175.0</td>
        </tr>
        <tr>
            <td>Edward Elmhurst Healthcare</td>
            <td>None</td>
            <td>IL</td>
            <td>175.0</td>
        </tr>
        <tr>
            <td>Augusta Health</td>
            <td>Fishersville</td>
            <td>VA</td>
            <td>176.0</td>
        </tr>
        <tr>
            <td>Houston Methodist</td>
            <td>None</td>
            <td>TX</td>
            <td>176.0</td>
        </tr>
        <tr>
            <td>Alta Bates Summit Medical Center</td>
            <td>Oakland</td>
            <td>CA</td>
            <td>177.0</td>
        </tr>
        <tr>
            <td>Intermountain Healthcare</td>
            <td>None</td>
            <td>ID</td>
            <td>177.0</td>
        </tr>
        <tr>
            <td>Appalachian Regional Healthcare System</td>
            <td>None</td>
            <td>NC</td>
            <td>178.0</td>
        </tr>
        <tr>
            <td>Community Hospital of Anaconda</td>
            <td>Anaconda</td>
            <td>MT</td>
            <td>178.0</td>
        </tr>
        <tr>
            <td>Northside Healthcare System</td>
            <td>None</td>
            <td>GA</td>
            <td>179.0</td>
        </tr>
        <tr>
            <td>Salem Hospital</td>
            <td>Salem</td>
            <td>OR</td>
            <td>179.0</td>
        </tr>
        <tr>
            <td>Kuakini Medical Center</td>
            <td>Honolulu</td>
            <td>HI</td>
            <td>180.0</td>
        </tr>
        <tr>
            <td>University of Texas Health System</td>
            <td>None</td>
            <td>TX</td>
            <td>180.0</td>
        </tr>
        <tr>
            <td>Cape Cod Healthcare</td>
            <td>None</td>
            <td>MA</td>
            <td>181.0</td>
        </tr>
        <tr>
            <td>GHS Hillcrest Memorial Hospital</td>
            <td>Simpsonville</td>
            <td>SC</td>
            <td>181.0</td>
        </tr>
        <tr>
            <td>Spectrum Health</td>
            <td>None</td>
            <td>MI</td>
            <td>182.0</td>
        </tr>
        <tr>
            <td>St. Marys Medical Center</td>
            <td>Grand Junction</td>
            <td>CO</td>
            <td>182.0</td>
        </tr>
        <tr>
            <td>Covenant Health</td>
            <td>None</td>
            <td>TN</td>
            <td>183.0</td>
        </tr>
        <tr>
            <td>Fort Sanders Regional Medical Center</td>
            <td>Knoxville</td>
            <td>TN</td>
            <td>183.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Miners Memorial Hospital</td>
            <td>Coaldale</td>
            <td>PA</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>UNC Health</td>
            <td>None</td>
            <td>NC</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>St. Vincent Charity Medical Center</td>
            <td>Cleveland</td>
            <td>OH</td>
            <td>185.0</td>
        </tr>
        <tr>
            <td>Tower Health</td>
            <td>None</td>
            <td>PA</td>
            <td>185.0</td>
        </tr>
        <tr>
            <td>CHI St. Alexius Health Dickinson</td>
            <td>Dickinson</td>
            <td>ND</td>
            <td>186.0</td>
        </tr>
        <tr>
            <td>Genesis Health System</td>
            <td>Silvis</td>
            <td>IL</td>
            <td>187.0</td>
        </tr>
        <tr>
            <td>Heritage Valley Health System</td>
            <td>None</td>
            <td>PA</td>
            <td>187.0</td>
        </tr>
        <tr>
            <td>Jefferson Health</td>
            <td>None</td>
            <td>NJ</td>
            <td>188.0</td>
        </tr>
        <tr>
            <td>Tacoma General Allenmore Hospital</td>
            <td>Tacoma</td>
            <td>WA</td>
            <td>188.0</td>
        </tr>
        <tr>
            <td>St. Anthony North Health Campus</td>
            <td>Westminster</td>
            <td>CO</td>
            <td>189.0</td>
        </tr>
        <tr>
            <td>North Austin Medical Center</td>
            <td>Austin</td>
            <td>TX</td>
            <td>190.0</td>
        </tr>
        <tr>
            <td>Samaritan Health Services</td>
            <td>None</td>
            <td>OR</td>
            <td>190.0</td>
        </tr>
        <tr>
            <td>Valley Medical Center</td>
            <td>Renton</td>
            <td>WA</td>
            <td>191.0</td>
        </tr>
        <tr>
            <td>Fairview Lakes Medical Center</td>
            <td>Wyoming</td>
            <td>MN</td>
            <td>192.0</td>
        </tr>
        <tr>
            <td>Health Quest Systems</td>
            <td>None</td>
            <td>CT</td>
            <td>192.0</td>
        </tr>
        <tr>
            <td>OHSU Hospital and Clinics</td>
            <td>Portland</td>
            <td>OR</td>
            <td>193.0</td>
        </tr>
        <tr>
            <td>St. Elizabeth Healthcare</td>
            <td>None</td>
            <td>IN</td>
            <td>193.0</td>
        </tr>
        <tr>
            <td>Mosaic Life Care</td>
            <td>None</td>
            <td>MO</td>
            <td>194.0</td>
        </tr>
        <tr>
            <td>Sutter Amador Hospital</td>
            <td>Jackson</td>
            <td>CA</td>
            <td>194.0</td>
        </tr>
        <tr>
            <td>Avera Health</td>
            <td>None</td>
            <td>MN</td>
            <td>195.0</td>
        </tr>
        <tr>
            <td>Providence Sacred Heart Medical Center and Children&#x27;s Hospital</td>
            <td>Spokane</td>
            <td>WA</td>
            <td>195.0</td>
        </tr>
        <tr>
            <td>Community Health Network</td>
            <td>None</td>
            <td>IN</td>
            <td>196.0</td>
        </tr>
        <tr>
            <td>Palm Bay Hospital</td>
            <td>Palm Bay</td>
            <td>FL</td>
            <td>196.0</td>
        </tr>
        <tr>
            <td>The Miriam Hospital</td>
            <td>Providence</td>
            <td>RI</td>
            <td>197.0</td>
        </tr>
        <tr>
            <td>LCMC Health System</td>
            <td>None</td>
            <td>LA</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>UPMC Jameson</td>
            <td>New Castle</td>
            <td>PA</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Holy Rosary Healthcare</td>
            <td>Miles City</td>
            <td>MT</td>
            <td>199.0</td>
        </tr>
        <tr>
            <td>Marshfield Clinic Health System</td>
            <td>None</td>
            <td>WI</td>
            <td>199.0</td>
        </tr>
        <tr>
            <td>Novant Health</td>
            <td>None</td>
            <td>NC</td>
            <td>200.0</td>
        </tr>
        <tr>
            <td>Marian Regional Medical Center</td>
            <td>Santa Maria</td>
            <td>CA</td>
            <td>201.0</td>
        </tr>
        <tr>
            <td>Methodist Le Bonheur Healthcare</td>
            <td>None</td>
            <td>MS</td>
            <td>201.0</td>
        </tr>
        <tr>
            <td>Ascension Eagle River Hospital</td>
            <td>Eagle River</td>
            <td>WI</td>
            <td>202.0</td>
        </tr>
        <tr>
            <td>Northeast Georgia Health System</td>
            <td>None</td>
            <td>GA</td>
            <td>202.0</td>
        </tr>
        <tr>
            <td>Henry Ford Health System</td>
            <td>None</td>
            <td>MI</td>
            <td>203.0</td>
        </tr>
        <tr>
            <td>Providence St. Mary Medical Center</td>
            <td>Walla Walla</td>
            <td>WA</td>
            <td>203.0</td>
        </tr>
        <tr>
            <td>University Hospitals Portage Medical Center</td>
            <td>Ravenna</td>
            <td>OH</td>
            <td>204.0</td>
        </tr>
        <tr>
            <td>Barton Memorial Hospital</td>
            <td>South Lake Tahoe</td>
            <td>CA</td>
            <td>205.0</td>
        </tr>
        <tr>
            <td>Cedars-Sinai Health System</td>
            <td>None</td>
            <td>CA</td>
            <td>205.0</td>
        </tr>
        <tr>
            <td>Franciscan Health</td>
            <td>None</td>
            <td>IL</td>
            <td>206.0</td>
        </tr>
        <tr>
            <td>UCSF Medical Center</td>
            <td>San Francisco</td>
            <td>CA</td>
            <td>206.0</td>
        </tr>
        <tr>
            <td>PIH Health</td>
            <td>None</td>
            <td>CA</td>
            <td>207.0</td>
        </tr>
        <tr>
            <td>Roxborough Memorial Hospital</td>
            <td>Philadelphia</td>
            <td>PA</td>
            <td>207.0</td>
        </tr>
        <tr>
            <td>Bay Park Community Hospital</td>
            <td>Oregon</td>
            <td>OH</td>
            <td>208.0</td>
        </tr>
        <tr>
            <td>Geisinger Health System</td>
            <td>None</td>
            <td>PA</td>
            <td>208.0</td>
        </tr>
        <tr>
            <td>Hilo Medical Center</td>
            <td>Hilo</td>
            <td>HI</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>McLaren Health Care Corporation</td>
            <td>None</td>
            <td>MI</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Sacred Heart Hospital</td>
            <td>Pensacola</td>
            <td>FL</td>
            <td>210.0</td>
        </tr>
        <tr>
            <td>TENET Healthcare Corporation</td>
            <td>None</td>
            <td>CA</td>
            <td>210.0</td>
        </tr>
        <tr>
            <td>Multicare Deaconess Hospital</td>
            <td>Spokane</td>
            <td>WA</td>
            <td>211.0</td>
        </tr>
        <tr>
            <td>West Virginia University Health System</td>
            <td>None</td>
            <td>OH</td>
            <td>211.0</td>
        </tr>
        <tr>
            <td>Premier Health</td>
            <td>None</td>
            <td>OH</td>
            <td>212.0</td>
        </tr>
        <tr>
            <td>Providence Medford Medical Center</td>
            <td>Medford</td>
            <td>OR</td>
            <td>212.0</td>
        </tr>
        <tr>
            <td>Cape Coral Hospital</td>
            <td>Cape Coral</td>
            <td>FL</td>
            <td>213.0</td>
        </tr>
        <tr>
            <td>Houston Healthcare</td>
            <td>None</td>
            <td>GA</td>
            <td>213.0</td>
        </tr>
        <tr>
            <td>Duke LifePoint Healthcare</td>
            <td>None</td>
            <td>NC</td>
            <td>214.0</td>
        </tr>
        <tr>
            <td>Round Rock Medical Center</td>
            <td>Round Rock</td>
            <td>TX</td>
            <td>214.0</td>
        </tr>
        <tr>
            <td>Guthrie Clinic</td>
            <td>None</td>
            <td>NY</td>
            <td>215.0</td>
        </tr>
        <tr>
            <td>Providence Centralia Hospital</td>
            <td>Centralia</td>
            <td>WA</td>
            <td>215.0</td>
        </tr>
        <tr>
            <td>Ochsner Health System</td>
            <td>None</td>
            <td>LA</td>
            <td>216.0</td>
        </tr>
        <tr>
            <td>Progress West Hospital</td>
            <td>O Fallon</td>
            <td>MO</td>
            <td>216.0</td>
        </tr>
        <tr>
            <td>Ephraim Mcdowell Health</td>
            <td>None</td>
            <td>KY</td>
            <td>217.0</td>
        </tr>
        <tr>
            <td>Excela Health Latrobe Hospital</td>
            <td>Latrobe</td>
            <td>PA</td>
            <td>217.0</td>
        </tr>
        <tr>
            <td>Munson Healthcare Grayling Hospital</td>
            <td>Grayling</td>
            <td>MI</td>
            <td>218.0</td>
        </tr>
        <tr>
            <td>Baptist Memorial Health Care Corporation</td>
            <td>None</td>
            <td>AR</td>
            <td>219.0</td>
        </tr>
        <tr>
            <td>Lake Huron Medical Center</td>
            <td>Port Huron</td>
            <td>MI</td>
            <td>219.0</td>
        </tr>
        <tr>
            <td>Memorial Health System</td>
            <td>None</td>
            <td>IL</td>
            <td>220.0</td>
        </tr>
        <tr>
            <td>Saint Joseph Regional Medical Center - Plymouth</td>
            <td>Plymouth</td>
            <td>IN</td>
            <td>220.0</td>
        </tr>
        <tr>
            <td>Adena Regional Medical Center</td>
            <td>Chillicothe</td>
            <td>OH</td>
            <td>221.0</td>
        </tr>
        <tr>
            <td>Owensboro Health</td>
            <td>None</td>
            <td>KY</td>
            <td>221.0</td>
        </tr>
        <tr>
            <td>Sentara RMH Medical Center</td>
            <td>Harrisonburg</td>
            <td>VA</td>
            <td>222.0</td>
        </tr>
        <tr>
            <td>Steward Health Care System</td>
            <td>None</td>
            <td>FL</td>
            <td>222.0</td>
        </tr>
        <tr>
            <td>CHI Health Creighton University Medical Center - Bergan Mercy</td>
            <td>Omaha</td>
            <td>NE</td>
            <td>223.0</td>
        </tr>
        <tr>
            <td>Emanate Health</td>
            <td>None</td>
            <td>CA</td>
            <td>223.0</td>
        </tr>
        <tr>
            <td>Roper Hospital</td>
            <td>Charleston</td>
            <td>SC</td>
            <td>224.0</td>
        </tr>
        <tr>
            <td>Medstar Southern Maryland Hospital Center</td>
            <td>Clinton</td>
            <td>MD</td>
            <td>225.0</td>
        </tr>
        <tr>
            <td>Southern Illinois Healthcare</td>
            <td>None</td>
            <td>IL</td>
            <td>225.0</td>
        </tr>
        <tr>
            <td>North Country Healthcare</td>
            <td>None</td>
            <td>NH</td>
            <td>226.0</td>
        </tr>
        <tr>
            <td>Wesley Medical Center</td>
            <td>Wichita</td>
            <td>KS</td>
            <td>226.0</td>
        </tr>
        <tr>
            <td>Franciscan Missionaries of Our Lady Health System</td>
            <td>None</td>
            <td>LA</td>
            <td>227.0</td>
        </tr>
        <tr>
            <td>Memorial Hermann Texas Medical Center</td>
            <td>Houston</td>
            <td>TX</td>
            <td>227.0</td>
        </tr>
        <tr>
            <td>Franciscan Health Lafayette</td>
            <td>Lafayette</td>
            <td>IN</td>
            <td>228.0</td>
        </tr>
        <tr>
            <td>Northern Light Health</td>
            <td>None</td>
            <td>ME</td>
            <td>228.0</td>
        </tr>
        <tr>
            <td>Lawrence &amp; Memorial Hospital</td>
            <td>New London</td>
            <td>CT</td>
            <td>229.0</td>
        </tr>
        <tr>
            <td>Los Angeles County Health Services Department</td>
            <td>None</td>
            <td>CA</td>
            <td>229.0</td>
        </tr>
        <tr>
            <td>McLaren Northern Michigan</td>
            <td>Petoskey</td>
            <td>MI</td>
            <td>230.0</td>
        </tr>
        <tr>
            <td>NYC Health + Hospitals</td>
            <td>None</td>
            <td>NY</td>
            <td>230.0</td>
        </tr>
        <tr>
            <td>Alameda Health System</td>
            <td>None</td>
            <td>CA</td>
            <td>231.0</td>
        </tr>
        <tr>
            <td>Atrium Health Lincoln</td>
            <td>Lincolnton</td>
            <td>NC</td>
            <td>231.0</td>
        </tr>
        <tr>
            <td>Archbold Medical Center</td>
            <td>None</td>
            <td>GA</td>
            <td>232.0</td>
        </tr>
        <tr>
            <td>Cox Medical Center Branson</td>
            <td>Branson</td>
            <td>MO</td>
            <td>232.0</td>
        </tr>
        <tr>
            <td>Medisys Health Network</td>
            <td>None</td>
            <td>NY</td>
            <td>233.0</td>
        </tr>
        <tr>
            <td>University of Virginia Medical Center</td>
            <td>Charlottesville</td>
            <td>VA</td>
            <td>233.0</td>
        </tr>
        <tr>
            <td>Erlanger Health System</td>
            <td>None</td>
            <td>NC</td>
            <td>234.0</td>
        </tr>
        <tr>
            <td>North Shore Medical Center -</td>
            <td>Salem</td>
            <td>MA</td>
            <td>234.0</td>
        </tr>
        <tr>
            <td>Alecto Healthcare</td>
            <td>None</td>
            <td>CA</td>
            <td>235.0</td>
        </tr>
        <tr>
            <td>Transylvania Regional Hospital</td>
            <td>Brevard</td>
            <td>NC</td>
            <td>235.0</td>
        </tr>
        <tr>
            <td>Cape Fear Valley Health System</td>
            <td>None</td>
            <td>NC</td>
            <td>236.0</td>
        </tr>
        <tr>
            <td>Mercy General Hospital</td>
            <td>Sacramento</td>
            <td>CA</td>
            <td>236.0</td>
        </tr>
        <tr>
            <td>Aultman Health Foundation</td>
            <td>None</td>
            <td>OH</td>
            <td>237.0</td>
        </tr>
        <tr>
            <td>Sutter Medical Center - Sacramento</td>
            <td>Sacramento</td>
            <td>CA</td>
            <td>237.0</td>
        </tr>
        <tr>
            <td>South Pointe Hospital</td>
            <td>Warrensville Heights</td>
            <td>OH</td>
            <td>238.0</td>
        </tr>
        <tr>
            <td>United Health Services</td>
            <td>None</td>
            <td>NY</td>
            <td>238.0</td>
        </tr>
        <tr>
            <td>St. Alexius Medical Center</td>
            <td>Hoffman Estates</td>
            <td>IL</td>
            <td>239.0</td>
        </tr>
        <tr>
            <td>Vidant Health</td>
            <td>None</td>
            <td>NC</td>
            <td>239.0</td>
        </tr>
        <tr>
            <td>Ministry Saint Mary&#x27;s Hospital</td>
            <td>Rhinelander</td>
            <td>WI</td>
            <td>240.0</td>
        </tr>
        <tr>
            <td>University of Mississippi Health Care</td>
            <td>None</td>
            <td>MS</td>
            <td>240.0</td>
        </tr>
        <tr>
            <td>Houston Methodist San Jacinto Hospital</td>
            <td>Baytown</td>
            <td>TX</td>
            <td>241.0</td>
        </tr>
        <tr>
            <td>Mohawk Valley Health System</td>
            <td>None</td>
            <td>NY</td>
            <td>241.0</td>
        </tr>
        <tr>
            <td>Lecom Health</td>
            <td>None</td>
            <td>PA</td>
            <td>242.0</td>
        </tr>
        <tr>
            <td>UPMC Northwest</td>
            <td>Seneca</td>
            <td>PA</td>
            <td>242.0</td>
        </tr>
        <tr>
            <td>Wellstar Cobb Hospital</td>
            <td>Austell</td>
            <td>GA</td>
            <td>243.0</td>
        </tr>
        <tr>
            <td>Marymount Hospital</td>
            <td>Garfield Heights</td>
            <td>OH</td>
            <td>244.0</td>
        </tr>
        <tr>
            <td>Olathe Health System</td>
            <td>None</td>
            <td>KS</td>
            <td>244.0</td>
        </tr>
        <tr>
            <td>Baylor Medical Center at Irving</td>
            <td>Irving</td>
            <td>TX</td>
            <td>245.0</td>
        </tr>
        <tr>
            <td>Community Healthcare System</td>
            <td>None</td>
            <td>IN</td>
            <td>245.0</td>
        </tr>
        <tr>
            <td>Chi Health Mercy Council Bluffs</td>
            <td>Council Bluffs</td>
            <td>IA</td>
            <td>246.0</td>
        </tr>
        <tr>
            <td>Mon Health</td>
            <td>None</td>
            <td>WV</td>
            <td>246.0</td>
        </tr>
        <tr>
            <td>North Mississippi Health Services</td>
            <td>None</td>
            <td>AL</td>
            <td>247.0</td>
        </tr>
        <tr>
            <td>UPMC Bedford Memorial</td>
            <td>Everett</td>
            <td>PA</td>
            <td>247.0</td>
        </tr>
        <tr>
            <td>Multicare Valley Hospital</td>
            <td>Spokane</td>
            <td>WA</td>
            <td>248.0</td>
        </tr>
        <tr>
            <td>UF Health</td>
            <td>None</td>
            <td>FL</td>
            <td>248.0</td>
        </tr>
        <tr>
            <td>Blessing Health System</td>
            <td>None</td>
            <td>IL</td>
            <td>249.0</td>
        </tr>
        <tr>
            <td>Las Palmas Medical Center</td>
            <td>El Paso</td>
            <td>TX</td>
            <td>249.0</td>
        </tr>
        <tr>
            <td>Hawkins County Memorial Hospital</td>
            <td>Rogersville</td>
            <td>TN</td>
            <td>250.0</td>
        </tr>
        <tr>
            <td>Mercy</td>
            <td>None</td>
            <td>AR</td>
            <td>250.0</td>
        </tr>
        <tr>
            <td>AdventHealth Waterman</td>
            <td>Tavares</td>
            <td>FL</td>
            <td>251.0</td>
        </tr>
        <tr>
            <td>Maury Regional Medical Center</td>
            <td>None</td>
            <td>TN</td>
            <td>252.0</td>
        </tr>
        <tr>
            <td>Methodist Medical Center of Oak Ridge</td>
            <td>Oak Ridge</td>
            <td>TN</td>
            <td>252.0</td>
        </tr>
        <tr>
            <td>Hospital Sisters Health System</td>
            <td>None</td>
            <td>IL</td>
            <td>253.0</td>
        </tr>
        <tr>
            <td>William W Backus Hospital</td>
            <td>Norwich</td>
            <td>CT</td>
            <td>253.0</td>
        </tr>
        <tr>
            <td>Mckay Dee Hospital</td>
            <td>Ogden</td>
            <td>UT</td>
            <td>254.0</td>
        </tr>
        <tr>
            <td>Nebraska Methodist Health System</td>
            <td>None</td>
            <td>IA</td>
            <td>254.0</td>
        </tr>
        <tr>
            <td>Gundersen Health System</td>
            <td>None</td>
            <td>IA</td>
            <td>255.0</td>
        </tr>
        <tr>
            <td>Advocate Trinity Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>256.0</td>
        </tr>
        <tr>
            <td>Easton Hospital</td>
            <td>Easton</td>
            <td>PA</td>
            <td>257.0</td>
        </tr>
        <tr>
            <td>Norton Healthcare</td>
            <td>None</td>
            <td>IN</td>
            <td>257.0</td>
        </tr>
        <tr>
            <td>Community Hospital Corporation</td>
            <td>None</td>
            <td>TX</td>
            <td>258.0</td>
        </tr>
        <tr>
            <td>Bon Secours Maryview Medical Center</td>
            <td>Portsmouth</td>
            <td>VA</td>
            <td>259.0</td>
        </tr>
        <tr>
            <td>Cox Health</td>
            <td>None</td>
            <td>MO</td>
            <td>259.0</td>
        </tr>
        <tr>
            <td>Baptist Health</td>
            <td>None</td>
            <td>AR</td>
            <td>260.0</td>
        </tr>
        <tr>
            <td>Presbyterian Espanola Hospital</td>
            <td>Espanola</td>
            <td>NM</td>
            <td>260.0</td>
        </tr>
        <tr>
            <td>Ardent Health Services</td>
            <td>None</td>
            <td>NJ</td>
            <td>261.0</td>
        </tr>
        <tr>
            <td>Banner - University Medical Center Phoenix</td>
            <td>Phoenix</td>
            <td>AZ</td>
            <td>261.0</td>
        </tr>
        <tr>
            <td>INTEGRIS Health</td>
            <td>None</td>
            <td>OK</td>
            <td>262.0</td>
        </tr>
        <tr>
            <td>Integris Bass Baptist Health Center</td>
            <td>Enid</td>
            <td>OK</td>
            <td>262.0</td>
        </tr>
        <tr>
            <td>Adventist Healthcare Washington Adventist Hospital</td>
            <td>Silver Spring</td>
            <td>MD</td>
            <td>263.0</td>
        </tr>
        <tr>
            <td>Eastside Medical Center</td>
            <td>Snellville</td>
            <td>GA</td>
            <td>264.0</td>
        </tr>
        <tr>
            <td>Infirmary Health System</td>
            <td>None</td>
            <td>AL</td>
            <td>264.0</td>
        </tr>
        <tr>
            <td>Banner Casa Grande Medical Center</td>
            <td>Casa Grande</td>
            <td>AZ</td>
            <td>265.0</td>
        </tr>
        <tr>
            <td>Huntsville Hospital Health System</td>
            <td>None</td>
            <td>AL</td>
            <td>265.0</td>
        </tr>
        <tr>
            <td>Dallas Medical Center</td>
            <td>Dallas</td>
            <td>TX</td>
            <td>266.0</td>
        </tr>
        <tr>
            <td>Penn Highlands Healthcare</td>
            <td>None</td>
            <td>PA</td>
            <td>266.0</td>
        </tr>
        <tr>
            <td>Novant Health UVA Health System Culpeper Medical Cente</td>
            <td>Culpeper</td>
            <td>VA</td>
            <td>267.0</td>
        </tr>
        <tr>
            <td>Union Health</td>
            <td>None</td>
            <td>IN</td>
            <td>267.0</td>
        </tr>
        <tr>
            <td>Atrium Health Cleveland</td>
            <td>Shelby</td>
            <td>NC</td>
            <td>268.0</td>
        </tr>
        <tr>
            <td>UNM Health</td>
            <td>None</td>
            <td>NM</td>
            <td>268.0</td>
        </tr>
        <tr>
            <td>Catholic Health Services of Long Island</td>
            <td>None</td>
            <td>NY</td>
            <td>269.0</td>
        </tr>
        <tr>
            <td>Desert Valley Hospital</td>
            <td>Victorville</td>
            <td>CA</td>
            <td>269.0</td>
        </tr>
        <tr>
            <td>Chi Health Good Samaritan</td>
            <td>Kearney</td>
            <td>NE</td>
            <td>270.0</td>
        </tr>
        <tr>
            <td>Mountain Health Network</td>
            <td>None</td>
            <td>WV</td>
            <td>271.0</td>
        </tr>
        <tr>
            <td>St. Vincent Evansville</td>
            <td>Evansville</td>
            <td>IN</td>
            <td>271.0</td>
        </tr>
        <tr>
            <td>Community Memorial Hospital San Buenaventura</td>
            <td>Ventura</td>
            <td>CA</td>
            <td>272.0</td>
        </tr>
        <tr>
            <td>UAB Health System</td>
            <td>None</td>
            <td>AL</td>
            <td>272.0</td>
        </tr>
        <tr>
            <td>Allen Hospital</td>
            <td>Waterloo</td>
            <td>IA</td>
            <td>273.0</td>
        </tr>
        <tr>
            <td>Holzer Health System</td>
            <td>None</td>
            <td>OH</td>
            <td>273.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>KY</td>
            <td>274.0</td>
        </tr>
        <tr>
            <td>Cumberland Medical Center</td>
            <td>Crossville</td>
            <td>TN</td>
            <td>275.0</td>
        </tr>
        <tr>
            <td>Arnot Health</td>
            <td>None</td>
            <td>NY</td>
            <td>276.0</td>
        </tr>
        <tr>
            <td>Medical Center of Lewisville</td>
            <td>Lewisville</td>
            <td>TX</td>
            <td>276.0</td>
        </tr>
        <tr>
            <td>Saint Francis Hospital South</td>
            <td>Tulsa</td>
            <td>OK</td>
            <td>277.0</td>
        </tr>
        <tr>
            <td>Spartanburg Regional Healthcare System</td>
            <td>None</td>
            <td>SC</td>
            <td>277.0</td>
        </tr>
        <tr>
            <td>Alamance Regional Medical Center</td>
            <td>Burlington</td>
            <td>NC</td>
            <td>278.0</td>
        </tr>
        <tr>
            <td>Southeast Georgia Health System</td>
            <td>None</td>
            <td>GA</td>
            <td>278.0</td>
        </tr>
        <tr>
            <td>Monument Health</td>
            <td>None</td>
            <td>SD</td>
            <td>279.0</td>
        </tr>
        <tr>
            <td>Tristar Summit Medical Center</td>
            <td>Hermitage</td>
            <td>TN</td>
            <td>279.0</td>
        </tr>
        <tr>
            <td>Cayuga Medical Center at Ithaca</td>
            <td>Ithaca</td>
            <td>NY</td>
            <td>280.0</td>
        </tr>
        <tr>
            <td>Willis-Knighton Health System</td>
            <td>None</td>
            <td>LA</td>
            <td>280.0</td>
        </tr>
        <tr>
            <td>Scripps Mercy Hospital</td>
            <td>San Diego</td>
            <td>CA</td>
            <td>281.0</td>
        </tr>
        <tr>
            <td>West Tennessee Healthcare</td>
            <td>None</td>
            <td>TN</td>
            <td>281.0</td>
        </tr>
        <tr>
            <td>High Point Regional Hospital</td>
            <td>High Point</td>
            <td>NC</td>
            <td>282.0</td>
        </tr>
        <tr>
            <td>McLeod Health</td>
            <td>None</td>
            <td>SC</td>
            <td>282.0</td>
        </tr>
        <tr>
            <td>Finger Lakes Health</td>
            <td>None</td>
            <td>NY</td>
            <td>283.0</td>
        </tr>
        <tr>
            <td>Utah Valley Hospital</td>
            <td>Provo</td>
            <td>UT</td>
            <td>283.0</td>
        </tr>
        <tr>
            <td>Freeman Health System</td>
            <td>None</td>
            <td>MO</td>
            <td>284.0</td>
        </tr>
        <tr>
            <td>Piedmont Henry Hospital</td>
            <td>Stockbridge</td>
            <td>GA</td>
            <td>284.0</td>
        </tr>
        <tr>
            <td>Licking Memorial Hospital</td>
            <td>Newark</td>
            <td>OH</td>
            <td>285.0</td>
        </tr>
        <tr>
            <td>St. Lawrence Health System</td>
            <td>None</td>
            <td>NY</td>
            <td>285.0</td>
        </tr>
        <tr>
            <td>Appalachian Regional Healthcare</td>
            <td>None</td>
            <td>KY</td>
            <td>286.0</td>
        </tr>
        <tr>
            <td>St. Anthony Community Hospital</td>
            <td>Warwick</td>
            <td>NY</td>
            <td>286.0</td>
        </tr>
        <tr>
            <td>Baton Rouge General Medical Center</td>
            <td>Baton Rouge</td>
            <td>LA</td>
            <td>287.0</td>
        </tr>
        <tr>
            <td>Commonwealth Health Corporation</td>
            <td>None</td>
            <td>KY</td>
            <td>287.0</td>
        </tr>
        <tr>
            <td>Phoebe Putney Health Systems</td>
            <td>None</td>
            <td>GA</td>
            <td>288.0</td>
        </tr>
        <tr>
            <td>Providence Little Company of Mary Medical Center - San Pedro</td>
            <td>San Pedro</td>
            <td>CA</td>
            <td>288.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>GA</td>
            <td>289.0</td>
        </tr>
        <tr>
            <td>West Florida Hospital</td>
            <td>Pensacola</td>
            <td>FL</td>
            <td>289.0</td>
        </tr>
        <tr>
            <td>Baptist Health South Florida</td>
            <td>None</td>
            <td>FL</td>
            <td>290.0</td>
        </tr>
        <tr>
            <td>GHSÂ¬â€  Laurens County Memorial Hospital</td>
            <td>Clinton</td>
            <td>SC</td>
            <td>290.0</td>
        </tr>
        <tr>
            <td>Broward Health</td>
            <td>None</td>
            <td>FL</td>
            <td>291.0</td>
        </tr>
        <tr>
            <td>Medical City Las Colinas</td>
            <td>Irving</td>
            <td>TX</td>
            <td>291.0</td>
        </tr>
        <tr>
            <td>Medical Center of Mckinney</td>
            <td>McKinney</td>
            <td>TX</td>
            <td>292.0</td>
        </tr>
        <tr>
            <td>White River Health System</td>
            <td>None</td>
            <td>AR</td>
            <td>292.0</td>
        </tr>
        <tr>
            <td>CHRISTUS Health</td>
            <td>None</td>
            <td>LA</td>
            <td>293.0</td>
        </tr>
        <tr>
            <td>St. John Owasso</td>
            <td>Owasso</td>
            <td>OK</td>
            <td>293.0</td>
        </tr>
        <tr>
            <td>Baptist Medical Center</td>
            <td>San Antonio</td>
            <td>TX</td>
            <td>294.0</td>
        </tr>
        <tr>
            <td>DCH Health System</td>
            <td>None</td>
            <td>AL</td>
            <td>294.0</td>
        </tr>
        <tr>
            <td>AdventHealth Sebring</td>
            <td>Sebring</td>
            <td>FL</td>
            <td>295.0</td>
        </tr>
        <tr>
            <td>Bassett Healthcare Network</td>
            <td>None</td>
            <td>NY</td>
            <td>295.0</td>
        </tr>
        <tr>
            <td>Bayshore Medical Center</td>
            <td>Holmdel</td>
            <td>NJ</td>
            <td>296.0</td>
        </tr>
        <tr>
            <td>LifeBridge Health</td>
            <td>None</td>
            <td>MD</td>
            <td>296.0</td>
        </tr>
        <tr>
            <td>Astria Health</td>
            <td>None</td>
            <td>WA</td>
            <td>297.0</td>
        </tr>
        <tr>
            <td>Trinity Rock Island</td>
            <td>Rock Island</td>
            <td>IL</td>
            <td>297.0</td>
        </tr>
        <tr>
            <td>Community First Medical Center</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>298.0</td>
        </tr>
        <tr>
            <td>WMCHealth</td>
            <td>None</td>
            <td>NY</td>
            <td>298.0</td>
        </tr>
        <tr>
            <td>Pampa Regional Medical Center</td>
            <td>Pampa</td>
            <td>TX</td>
            <td>299.0</td>
        </tr>
        <tr>
            <td>Good Samaritan Regional Health Center</td>
            <td>Mount Vernon</td>
            <td>IL</td>
            <td>300.0</td>
        </tr>
        <tr>
            <td>MidMichigan Health</td>
            <td>None</td>
            <td>MI</td>
            <td>300.0</td>
        </tr>
        <tr>
            <td>Flagstaff Medical Center</td>
            <td>Flagstaff</td>
            <td>AZ</td>
            <td>301.0</td>
        </tr>
        <tr>
            <td>Forrest Health</td>
            <td>None</td>
            <td>MS</td>
            <td>301.0</td>
        </tr>
        <tr>
            <td>Beebe Medical Center</td>
            <td>Lewes</td>
            <td>DE</td>
            <td>302.0</td>
        </tr>
        <tr>
            <td>Rush Health Systems</td>
            <td>None</td>
            <td>MS</td>
            <td>302.0</td>
        </tr>
        <tr>
            <td>Promedica Monroe Regional Hospital</td>
            <td>Monroe</td>
            <td>MI</td>
            <td>303.0</td>
        </tr>
        <tr>
            <td>Lovelace Regional Hospital - Roswell</td>
            <td>Roswell</td>
            <td>NM</td>
            <td>304.0</td>
        </tr>
        <tr>
            <td>Tanner Health System</td>
            <td>None</td>
            <td>GA</td>
            <td>304.0</td>
        </tr>
        <tr>
            <td>Saint Bernards Healthcare</td>
            <td>None</td>
            <td>AR</td>
            <td>305.0</td>
        </tr>
        <tr>
            <td>Seton Medical Center</td>
            <td>Daly City</td>
            <td>CA</td>
            <td>305.0</td>
        </tr>
        <tr>
            <td>Tift Regional Health System</td>
            <td>None</td>
            <td>GA</td>
            <td>306.0</td>
        </tr>
        <tr>
            <td>Beatrice Community Hospital &amp; Health Center</td>
            <td>Beatrice</td>
            <td>NE</td>
            <td>307.0</td>
        </tr>
        <tr>
            <td>Eskenazi Health</td>
            <td>Indianapolis</td>
            <td>IN</td>
            <td>308.0</td>
        </tr>
        <tr>
            <td>Harlem Hospital Center</td>
            <td>New York</td>
            <td>NY</td>
            <td>309.0</td>
        </tr>
        <tr>
            <td>Miners&#x27; Colfax Medical Center</td>
            <td>Raton</td>
            <td>NM</td>
            <td>310.0</td>
        </tr>
        <tr>
            <td>Champlain Valley Physicians Hospital Medical Center</td>
            <td>Plattsburgh</td>
            <td>NY</td>
            <td>311.0</td>
        </tr>
        <tr>
            <td>Woodhull Medical and Mental Health Center</td>
            <td>Brooklyn</td>
            <td>NY</td>
            <td>312.0</td>
        </tr>
        <tr>
            <td>Temple University Hospital</td>
            <td>Philadelphia</td>
            <td>PA</td>
            <td>313.0</td>
        </tr>
        <tr>
            <td>LAC+USC Medical Center</td>
            <td>Los Angeles</td>
            <td>CA</td>
            <td>314.0</td>
        </tr>
        <tr>
            <td>Contra Costa Regional Medical Center</td>
            <td>Martinez</td>
            <td>CA</td>
            <td>315.0</td>
        </tr>
        <tr>
            <td>Arrowhead Regional Medical Center</td>
            <td>Colton</td>
            <td>CA</td>
            <td>316.0</td>
        </tr>
        <tr>
            <td>Mt. Sinai Hospital Medical Center</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>317.0</td>
        </tr>
        <tr>
            <td>Westfields Hospital and Clinic</td>
            <td>New Richmond</td>
            <td>WI</td>
            <td>318.0</td>
        </tr>
        <tr>
            <td>Franklin Regional Hospital</td>
            <td>Franklin</td>
            <td>NH</td>
            <td>319.0</td>
        </tr>
        <tr>
            <td>Lincoln Medical &amp; Mental Health Center</td>
            <td>Bronx</td>
            <td>NY</td>
            <td>320.0</td>
        </tr>
        <tr>
            <td>Sutter Lakeside Hospital</td>
            <td>Lakeport</td>
            <td>CA</td>
            <td>321.0</td>
        </tr>
        <tr>
            <td>Regional Medical Center of San Jose</td>
            <td>San Jose</td>
            <td>CA</td>
            <td>322.0</td>
        </tr>
        <tr>
            <td>Thedacare Medical Center New London</td>
            <td>New London</td>
            <td>WI</td>
            <td>323.0</td>
        </tr>
        <tr>
            <td>St. Johns Regional Medical Center</td>
            <td>Oxnard</td>
            <td>CA</td>
            <td>324.0</td>
        </tr>
        <tr>
            <td>Capital Health Regional Medical Center</td>
            <td>Trenton</td>
            <td>NJ</td>
            <td>325.0</td>
        </tr>
        <tr>
            <td>Cambridge Health Alliance</td>
            <td>Cambridge</td>
            <td>MA</td>
            <td>327.0</td>
        </tr>
        <tr>
            <td>Samaritan Albany General Hospital</td>
            <td>Albany</td>
            <td>OR</td>
            <td>328.0</td>
        </tr>
        <tr>
            <td>North Central Bronx Hospital</td>
            <td>Bronx</td>
            <td>NY</td>
            <td>329.0</td>
        </tr>
        <tr>
            <td>Adventist Health Tillamook</td>
            <td>Tillamook</td>
            <td>OR</td>
            <td>330.0</td>
        </tr>
        <tr>
            <td>Bedford Memorial Hospital</td>
            <td>Bedford</td>
            <td>VA</td>
            <td>331.0</td>
        </tr>
        <tr>
            <td>Oroville Hospital</td>
            <td>Oroville</td>
            <td>CA</td>
            <td>332.0</td>
        </tr>
        <tr>
            <td>United Medical Center</td>
            <td>Washington</td>
            <td>DC</td>
            <td>333.0</td>
        </tr>
        <tr>
            <td>The Nebraska Medical Center</td>
            <td>Omaha</td>
            <td>NE</td>
            <td>334.0</td>
        </tr>
        <tr>
            <td>Southwest Memorial Hospital</td>
            <td>Cortez</td>
            <td>CO</td>
            <td>335.0</td>
        </tr>
        <tr>
            <td>Banner Churchill Community Hospital</td>
            <td>Fallon</td>
            <td>NV</td>
            <td>336.0</td>
        </tr>
        <tr>
            <td>Hennepin Healthcare - HCMC</td>
            <td>Minneapolis</td>
            <td>MN</td>
            <td>337.0</td>
        </tr>
        <tr>
            <td>Samaritan Lebanon Community Hospital</td>
            <td>Lebanon</td>
            <td>OR</td>
            <td>338.0</td>
        </tr>
        <tr>
            <td>Bronx-Lebanon Hospital Center</td>
            <td>Bronx</td>
            <td>NY</td>
            <td>339.0</td>
        </tr>
        <tr>
            <td>Sutter Delta Medical Center</td>
            <td>Antioch</td>
            <td>CA</td>
            <td>340.0</td>
        </tr>
        <tr>
            <td>Carilion Franklin Memorial Hospital</td>
            <td>Rocky Mount</td>
            <td>VA</td>
            <td>341.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital of Gardena</td>
            <td>Gardena</td>
            <td>CA</td>
            <td>342.0</td>
        </tr>
        <tr>
            <td>Mercy Fitzgerald Hospital</td>
            <td>Darby</td>
            <td>PA</td>
            <td>343.0</td>
        </tr>
        <tr>
            <td>St. Mary&#x27;s Hospital at Amsterdam</td>
            <td>Amsterdam</td>
            <td>NY</td>
            <td>344.0</td>
        </tr>
        <tr>
            <td>Androscoggin Valley Hospital</td>
            <td>Berlin</td>
            <td>NH</td>
            <td>345.0</td>
        </tr>
        <tr>
            <td>Santa Clara Valley Medical Center</td>
            <td>San Jose</td>
            <td>CA</td>
            <td>346.0</td>
        </tr>
        <tr>
            <td>University of Kentucky Hospital</td>
            <td>Lexington</td>
            <td>KY</td>
            <td>347.0</td>
        </tr>
        <tr>
            <td>Southern California Hospital at Hollywood</td>
            <td>Hollywood</td>
            <td>CA</td>
            <td>348.0</td>
        </tr>
        <tr>
            <td>Saint Francis Memorial Hospital</td>
            <td>San Francisco</td>
            <td>CA</td>
            <td>349.0</td>
        </tr>
        <tr>
            <td>Saint James Hospital</td>
            <td>Pontiac</td>
            <td>IL</td>
            <td>350.0</td>
        </tr>
        <tr>
            <td>Clifton Springs Hospital and Clinic</td>
            <td>Clifton Springs</td>
            <td>NY</td>
            <td>351.0</td>
        </tr>
        <tr>
            <td>Osceola Regional Medical Center</td>
            <td>Kissimmee</td>
            <td>FL</td>
            <td>352.0</td>
        </tr>
        <tr>
            <td>Erie County Medical Center</td>
            <td>Buffalo</td>
            <td>NY</td>
            <td>353.0</td>
        </tr>
        <tr>
            <td>Seton Highland Lakes</td>
            <td>Burnet</td>
            <td>TX</td>
            <td>355.0</td>
        </tr>
        <tr>
            <td>University of California Irvine Medical Center</td>
            <td>Orange</td>
            <td>CA</td>
            <td>356.0</td>
        </tr>
        <tr>
            <td>Los Angeles Community Hospital</td>
            <td>Los Angeles</td>
            <td>CA</td>
            <td>357.0</td>
        </tr>
        <tr>
            <td>California Hospital Medical Center LA</td>
            <td>Los Angeles</td>
            <td>CA</td>
            <td>358.0</td>
        </tr>
        <tr>
            <td>St. Barnabas Hospital</td>
            <td>Bronx</td>
            <td>NY</td>
            <td>359.0</td>
        </tr>
        <tr>
            <td>New Orleans East Hospital</td>
            <td>New Orleans</td>
            <td>LA</td>
            <td>360.0</td>
        </tr>
        <tr>
            <td>Mission Regional Medical Center</td>
            <td>Mission</td>
            <td>TX</td>
            <td>361.0</td>
        </tr>
        <tr>
            <td>Frisbie Memorial Hospital</td>
            <td>Rochester</td>
            <td>NH</td>
            <td>362.0</td>
        </tr>
        <tr>
            <td>Hurley Medical Center</td>
            <td>Flint</td>
            <td>MI</td>
            <td>363.0</td>
        </tr>
        <tr>
            <td>Summa Health System</td>
            <td>Akron</td>
            <td>OH</td>
            <td>364.0</td>
        </tr>
        <tr>
            <td>Natividad Medical Center</td>
            <td>Salinas</td>
            <td>CA</td>
            <td>365.0</td>
        </tr>
        <tr>
            <td>Saint Peter&#x27;s University Hospital</td>
            <td>New Brunswick</td>
            <td>NJ</td>
            <td>366.0</td>
        </tr>
        <tr>
            <td>Leonard J Chabert Medical Center</td>
            <td>Houma</td>
            <td>LA</td>
            <td>367.0</td>
        </tr>
        <tr>
            <td>Banner Goldfield Medical Center</td>
            <td>Apache Junction</td>
            <td>AZ</td>
            <td>368.0</td>
        </tr>
        <tr>
            <td>Fort Loudon Medical Center</td>
            <td>Lenoir City</td>
            <td>TN</td>
            <td>369.0</td>
        </tr>
        <tr>
            <td>Rutland Regional Medical Center</td>
            <td>Rutland</td>
            <td>VT</td>
            <td>371.0</td>
        </tr>
        <tr>
            <td>Summit Healthcare Regional Medical Center</td>
            <td>Show Low</td>
            <td>AZ</td>
            <td>372.0</td>
        </tr>
        <tr>
            <td>Baptist Memorial Hospital North MS</td>
            <td>Oxford</td>
            <td>MS</td>
            <td>373.0</td>
        </tr>
        <tr>
            <td>Waldo County General Hospital</td>
            <td>Belfast</td>
            <td>ME</td>
            <td>374.0</td>
        </tr>
        <tr>
            <td>St. Croix Regional Medical Center</td>
            <td>Saint Croix Falls</td>
            <td>WI</td>
            <td>375.0</td>
        </tr>
        <tr>
            <td>Wellstar Douglas Hospital</td>
            <td>Douglasville</td>
            <td>GA</td>
            <td>376.0</td>
        </tr>
        <tr>
            <td>University of Mississippi Medical Center</td>
            <td>Jackson</td>
            <td>MS</td>
            <td>377.0</td>
        </tr>
        <tr>
            <td>Mason General Hospital &amp; Family of Clinics</td>
            <td>Shelton</td>
            <td>WA</td>
            <td>378.0</td>
        </tr>
        <tr>
            <td>Knapp Medical Center</td>
            <td>Weslaco</td>
            <td>TX</td>
            <td>379.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System - Lake City</td>
            <td>Lake City</td>
            <td>MN</td>
            <td>380.0</td>
        </tr>
        <tr>
            <td>Lincoln County Medical Center</td>
            <td>Ruidoso</td>
            <td>NM</td>
            <td>381.0</td>
        </tr>
        <tr>
            <td>Northeastern Vermont Regional Hospital</td>
            <td>Saint Johnsbury</td>
            <td>VT</td>
            <td>382.0</td>
        </tr>
        <tr>
            <td>Doctors Medical Center</td>
            <td>Modesto</td>
            <td>CA</td>
            <td>384.0</td>
        </tr>
        <tr>
            <td>Sinai-Grace Hospital</td>
            <td>Detroit</td>
            <td>MI</td>
            <td>385.0</td>
        </tr>
        <tr>
            <td>Montefiore Mount Vernon Hospital</td>
            <td>Mount Vernon</td>
            <td>NY</td>
            <td>386.0</td>
        </tr>
        <tr>
            <td>T. J. Samson Community Hospital</td>
            <td>Glasgow</td>
            <td>KY</td>
            <td>387.0</td>
        </tr>
        <tr>
            <td>Samaritan North Lincoln Hospital</td>
            <td>Lincoln City</td>
            <td>OR</td>
            <td>388.0</td>
        </tr>
        <tr>
            <td>PeacHealth St. John Medical Center</td>
            <td>Longview</td>
            <td>WA</td>
            <td>389.0</td>
        </tr>
        <tr>
            <td>Rio Grande Regional Hospital</td>
            <td>McAllen</td>
            <td>TX</td>
            <td>390.0</td>
        </tr>
        <tr>
            <td>Twin Cities Community Hospital</td>
            <td>Templeton</td>
            <td>CA</td>
            <td>391.0</td>
        </tr>
        <tr>
            <td>Kings County Hospital Center</td>
            <td>Brooklyn</td>
            <td>NY</td>
            <td>392.0</td>
        </tr>
        <tr>
            <td>Ascension St. Francis Hospital</td>
            <td>Milwaukee</td>
            <td>WI</td>
            <td>393.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Washington</td>
            <td>Washington</td>
            <td>MO</td>
            <td>394.0</td>
        </tr>
        <tr>
            <td>Atlantic General Hospital</td>
            <td>Berlin</td>
            <td>MD</td>
            <td>395.0</td>
        </tr>
        <tr>
            <td>Falmouth Hospital</td>
            <td>Falmouth</td>
            <td>MA</td>
            <td>396.0</td>
        </tr>
        <tr>
            <td>Northwestern Medical Center Inc</td>
            <td>Saint Albans</td>
            <td>VT</td>
            <td>397.0</td>
        </tr>
        <tr>
            <td>Springhill Medical Center</td>
            <td>Springhill</td>
            <td>LA</td>
            <td>398.0</td>
        </tr>
        <tr>
            <td>Truman Medical Center Lakewood</td>
            <td>Kansas City</td>
            <td>MO</td>
            <td>399.0</td>
        </tr>
        <tr>
            <td>Mile Bluff Medical Center</td>
            <td>Mauston</td>
            <td>WI</td>
            <td>400.0</td>
        </tr>
        <tr>
            <td>Grande Ronde Hospital</td>
            <td>O&#x27;Neill</td>
            <td>OR</td>
            <td>401.0</td>
        </tr>
        <tr>
            <td>Samaritan Pacific Community Hospital</td>
            <td>Newport</td>
            <td>OR</td>
            <td>402.0</td>
        </tr>
        <tr>
            <td>Weeks Medical Center</td>
            <td>Lancaster</td>
            <td>NH</td>
            <td>403.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital, The</td>
            <td>Craig</td>
            <td>CO</td>
            <td>404.0</td>
        </tr>
        <tr>
            <td>Advocate EurekaÂ¬â€ Hospital</td>
            <td>Eureka</td>
            <td>IL</td>
            <td>405.0</td>
        </tr>
        <tr>
            <td>Cambridge Medical Center</td>
            <td>Cambridge</td>
            <td>MN</td>
            <td>406.0</td>
        </tr>
        <tr>
            <td>New Ulm Medical Center</td>
            <td>New Ulm</td>
            <td>MN</td>
            <td>407.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System Eau Claire</td>
            <td>Eau Claire</td>
            <td>WI</td>
            <td>408.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Hospital Rochester</td>
            <td>Rochester</td>
            <td>MN</td>
            <td>409.0</td>
        </tr>
        <tr>
            <td>Olmsted Medical Center</td>
            <td>Rochester</td>
            <td>MN</td>
            <td>410.0</td>
        </tr>
        <tr>
            <td>Great Falls Clinic Hospital</td>
            <td>Great Falls</td>
            <td>MT</td>
            <td>411.0</td>
        </tr>
        <tr>
            <td>Fort Memorial Hospital</td>
            <td>Fort Atkinson</td>
            <td>WI</td>
            <td>412.0</td>
        </tr>
        <tr>
            <td>Avera Queen of Peace</td>
            <td>Mitchell</td>
            <td>SD</td>
            <td>413.0</td>
        </tr>
        <tr>
            <td>University of Utah Hospitals and Clinics</td>
            <td>Salt Lake City</td>
            <td>UT</td>
            <td>414.0</td>
        </tr>
        <tr>
            <td>Sentara Leigh Hospital</td>
            <td>Norfolk</td>
            <td>VA</td>
            <td>415.0</td>
        </tr>
        <tr>
            <td>Providence Medical Center</td>
            <td>Kansas City</td>
            <td>KS</td>
            <td>416.0</td>
        </tr>
        <tr>
            <td>Maple Grove Hospital</td>
            <td>Maple Grove</td>
            <td>MN</td>
            <td>418.0</td>
        </tr>
        <tr>
            <td>Centura Health-Penrose St. Francis Health Services</td>
            <td>Colorado Springs</td>
            <td>CO</td>
            <td>419.0</td>
        </tr>
        <tr>
            <td>Virginia Mason Medical Center</td>
            <td>Seattle</td>
            <td>WA</td>
            <td>420.0</td>
        </tr>
        <tr>
            <td>Bear River Valley Hospital</td>
            <td>Tremonton</td>
            <td>UT</td>
            <td>421.0</td>
        </tr>
        <tr>
            <td>Legacy Meridian Park Medical Center</td>
            <td>Tualatin</td>
            <td>OR</td>
            <td>422.0</td>
        </tr>
        <tr>
            <td>Pennsylvania Hospital</td>
            <td>Philadelphia</td>
            <td>PA</td>
            <td>423.0</td>
        </tr>
        <tr>
            <td>Lancaster General Hospital</td>
            <td>Lancaster</td>
            <td>PA</td>
            <td>424.0</td>
        </tr>
        <tr>
            <td>Alta View Hospital</td>
            <td>Sandy</td>
            <td>UT</td>
            <td>425.0</td>
        </tr>
        <tr>
            <td>Baylor Scott &amp; White Medical Center - Taylor</td>
            <td>Taylor</td>
            <td>TX</td>
            <td>426.0</td>
        </tr>
        <tr>
            <td>EvergreenHealth Medical Center</td>
            <td>Kirkland</td>
            <td>WA</td>
            <td>427.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System - Franciscan Medical Center</td>
            <td>La Crosse</td>
            <td>WI</td>
            <td>428.0</td>
        </tr>
        <tr>
            <td>Mountain View Hospital</td>
            <td>Payson</td>
            <td>UT</td>
            <td>429.0</td>
        </tr>
        <tr>
            <td>St. Cloud Hospital</td>
            <td>Saint Cloud</td>
            <td>MN</td>
            <td>430.0</td>
        </tr>
        <tr>
            <td>Boone Hospital Center</td>
            <td>Columbia</td>
            <td>MO</td>
            <td>431.0</td>
        </tr>
        <tr>
            <td>North Memorial Health</td>
            <td>Robbinsdale</td>
            <td>MN</td>
            <td>432.0</td>
        </tr>
        <tr>
            <td>AdventHealth Hendersonville</td>
            <td>Hendersonville</td>
            <td>NC</td>
            <td>433.0</td>
        </tr>
        <tr>
            <td>Northern Light Inland Hospital</td>
            <td>Waterville</td>
            <td>ME</td>
            <td>434.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Hospital - Anderson Campus</td>
            <td>Easton</td>
            <td>PA</td>
            <td>435.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Hospital</td>
            <td>Duluth</td>
            <td>MN</td>
            <td>436.0</td>
        </tr>
        <tr>
            <td>Mary Rutan Hospital</td>
            <td>Bellefontaine</td>
            <td>OH</td>
            <td>437.0</td>
        </tr>
        <tr>
            <td>River Falls Area Hospital</td>
            <td>River Falls</td>
            <td>WI</td>
            <td>438.0</td>
        </tr>
        <tr>
            <td>The Queens Medical Center</td>
            <td>Honolulu</td>
            <td>HI</td>
            <td>439.0</td>
        </tr>
        <tr>
            <td>Redmond Regional Medical Center</td>
            <td>Rome</td>
            <td>GA</td>
            <td>440.0</td>
        </tr>
        <tr>
            <td>Oaklawn Hospital</td>
            <td>Marshall</td>
            <td>MI</td>
            <td>441.0</td>
        </tr>
        <tr>
            <td>Highland Hospital</td>
            <td>Rochester</td>
            <td>NY</td>
            <td>442.0</td>
        </tr>
        <tr>
            <td>UC San Diego Health - Hillcrest Medical Center</td>
            <td>San Diego</td>
            <td>CA</td>
            <td>443.0</td>
        </tr>
        <tr>
            <td>CHI Lisbon Health</td>
            <td>Lisbon</td>
            <td>ND</td>
            <td>444.0</td>
        </tr>
        <tr>
            <td>Logan Regional Hospital</td>
            <td>Logan</td>
            <td>UT</td>
            <td>445.0</td>
        </tr>
        <tr>
            <td>Providence St. Vincent Medical Center</td>
            <td>Portland</td>
            <td>OR</td>
            <td>446.0</td>
        </tr>
        <tr>
            <td>Abbott Northwestern Hospital</td>
            <td>Minneapolis</td>
            <td>MN</td>
            <td>447.0</td>
        </tr>
        <tr>
            <td>Regina Hospital</td>
            <td>Hastings</td>
            <td>MN</td>
            <td>448.0</td>
        </tr>
        <tr>
            <td>Pali Momi Medical Center</td>
            <td>Aiea</td>
            <td>HI</td>
            <td>449.0</td>
        </tr>
        <tr>
            <td>Straub Clinic and Hospital</td>
            <td>Honolulu</td>
            <td>HI</td>
            <td>450.0</td>
        </tr>
        <tr>
            <td>SSM Health St. Mary&#x27;s Hospital - Madison</td>
            <td>Madison</td>
            <td>WI</td>
            <td>451.0</td>
        </tr>
        <tr>
            <td>Sonoma Valley Hospital</td>
            <td>Sonoma</td>
            <td>CA</td>
            <td>452.0</td>
        </tr>
        <tr>
            <td>Ascension Calumet Hospital</td>
            <td>Chilton</td>
            <td>WI</td>
            <td>453.0</td>
        </tr>
        <tr>
            <td>SSM Health St. Mary&#x27;s Hospital - Janesville</td>
            <td>Janesville</td>
            <td>WI</td>
            <td>454.0</td>
        </tr>
        <tr>
            <td>Fairview Ridges Hospital</td>
            <td>Burnsville</td>
            <td>MN</td>
            <td>455.0</td>
        </tr>
        <tr>
            <td>Wellspan Ephrata Community Hospital</td>
            <td>Ephrata</td>
            <td>PA</td>
            <td>456.0</td>
        </tr>
        <tr>
            <td>Swedish Medical Center</td>
            <td>Seattle</td>
            <td>WA</td>
            <td>457.0</td>
        </tr>
        <tr>
            <td>Monument Health Spearfish Hospital</td>
            <td>Spearfish</td>
            <td>SD</td>
            <td>458.0</td>
        </tr>
        <tr>
            <td>Mercy Health - Willard Hospital</td>
            <td>Willard</td>
            <td>OH</td>
            <td>459.0</td>
        </tr>
        <tr>
            <td>Covenant Hospital Plainview</td>
            <td>Plainview</td>
            <td>TX</td>
            <td>460.0</td>
        </tr>
        <tr>
            <td>Avera Sacred Heart Hospital</td>
            <td>Yankton</td>
            <td>SD</td>
            <td>461.0</td>
        </tr>
        <tr>
            <td>Asante Ashland Community Hospital</td>
            <td>Ashland</td>
            <td>OR</td>
            <td>462.0</td>
        </tr>
        <tr>
            <td>Community Medical Center</td>
            <td>Missoula</td>
            <td>MT</td>
            <td>463.0</td>
        </tr>
        <tr>
            <td>Suburban Community Hospital</td>
            <td>Norristown</td>
            <td>PA</td>
            <td>464.0</td>
        </tr>
        <tr>
            <td>University of Kansas Hospital</td>
            <td>Kansas City</td>
            <td>KS</td>
            <td>466.0</td>
        </tr>
        <tr>
            <td>Saint Mary&#x27;s Health Care</td>
            <td>Grand Rapids</td>
            <td>MI</td>
            <td>467.0</td>
        </tr>
        <tr>
            <td>St. Joseph Mercy Chelsea</td>
            <td>Chelsea</td>
            <td>MI</td>
            <td>468.0</td>
        </tr>
        <tr>
            <td>Yakima Valley Memorial Hospital</td>
            <td>Yakima</td>
            <td>WA</td>
            <td>469.0</td>
        </tr>
        <tr>
            <td>St. Peter&#x27;s Hospital</td>
            <td>Albany</td>
            <td>NY</td>
            <td>470.0</td>
        </tr>
        <tr>
            <td>Sentara Northern Virginia Medical Center</td>
            <td>Woodbridge</td>
            <td>VA</td>
            <td>471.0</td>
        </tr>
        <tr>
            <td>Legacy Silverton Medical Center</td>
            <td>Silverton</td>
            <td>OR</td>
            <td>472.0</td>
        </tr>
        <tr>
            <td>American Fork Hospital</td>
            <td>American Fork</td>
            <td>UT</td>
            <td>473.0</td>
        </tr>
        <tr>
            <td>Intermountain Medical Center</td>
            <td>Murray</td>
            <td>UT</td>
            <td>474.0</td>
        </tr>
        <tr>
            <td>Ascension Borgess Hospital</td>
            <td>Kalamazoo</td>
            <td>MI</td>
            <td>475.0</td>
        </tr>
        <tr>
            <td>Ascension Columbia St. Mary&#x27;s Hospital Milwaukee</td>
            <td>Milwaukee</td>
            <td>WI</td>
            <td>476.0</td>
        </tr>
        <tr>
            <td>Martha Jefferson Hospital</td>
            <td>Charlottesville</td>
            <td>VA</td>
            <td>477.0</td>
        </tr>
        <tr>
            <td>Olympic Medical Center</td>
            <td>Port Angeles</td>
            <td>WA</td>
            <td>478.0</td>
        </tr>
        <tr>
            <td>Saint Mary&#x27;s Regional Medical Center</td>
            <td>Reno</td>
            <td>NV</td>
            <td>479.0</td>
        </tr>
        <tr>
            <td>Baylor Scott &amp; White Medical Center - Marble Falls</td>
            <td>Marble Falls</td>
            <td>TX</td>
            <td>480.0</td>
        </tr>
        <tr>
            <td>Greene Memorial Hospital</td>
            <td>Xenia</td>
            <td>OH</td>
            <td>481.0</td>
        </tr>
        <tr>
            <td>Mercy Health - West Hospital</td>
            <td>Cincinnati</td>
            <td>OH</td>
            <td>482.0</td>
        </tr>
        <tr>
            <td>UnityPoint Health - Meriter</td>
            <td>Madison</td>
            <td>WI</td>
            <td>483.0</td>
        </tr>
        <tr>
            <td>CHI HealthÂ¬â€  - Mercy Corning</td>
            <td>Corning</td>
            <td>IA</td>
            <td>484.0</td>
        </tr>
        <tr>
            <td>Providence Hood River Memorial Hospital</td>
            <td>Hood River</td>
            <td>OR</td>
            <td>485.0</td>
        </tr>
        <tr>
            <td>Sherman Hospital</td>
            <td>Elgin</td>
            <td>IL</td>
            <td>486.0</td>
        </tr>
        <tr>
            <td>Maine Medical Center</td>
            <td>Portland</td>
            <td>ME</td>
            <td>487.0</td>
        </tr>
        <tr>
            <td>Sutter Auburn Faith Hospital</td>
            <td>Auburn</td>
            <td>CA</td>
            <td>488.0</td>
        </tr>
        <tr>
            <td>North Hawaii Community Hospital</td>
            <td>Kamuela</td>
            <td>HI</td>
            <td>489.0</td>
        </tr>
        <tr>
            <td>HCA Houston Healthcare West</td>
            <td>Houston</td>
            <td>TX</td>
            <td>490.0</td>
        </tr>
        <tr>
            <td>Bon Secours St. Marys Hospital</td>
            <td>Richmond</td>
            <td>VA</td>
            <td>491.0</td>
        </tr>
        <tr>
            <td>Sentara Norfolk General Hospital</td>
            <td>Norfolk</td>
            <td>VA</td>
            <td>492.0</td>
        </tr>
        <tr>
            <td>Rex Hospital</td>
            <td>Raleigh</td>
            <td>NC</td>
            <td>493.0</td>
        </tr>
        <tr>
            <td>Sentara Williamsburg Regional Medical Center</td>
            <td>Williamsburg</td>
            <td>VA</td>
            <td>494.0</td>
        </tr>
        <tr>
            <td>St. Mark&#x27;s Hospital</td>
            <td>Salt Lake City</td>
            <td>UT</td>
            <td>495.0</td>
        </tr>
        <tr>
            <td>Presence Resurrection Medical Center</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>497.0</td>
        </tr>
        <tr>
            <td>Rose Medical Center</td>
            <td>Denver</td>
            <td>CO</td>
            <td>498.0</td>
        </tr>
        <tr>
            <td>Santa Ynez Valley Cottage Hospital</td>
            <td>Solvang</td>
            <td>CA</td>
            <td>499.0</td>
        </tr>
        <tr>
            <td>Providence Alaska Medical Center</td>
            <td>Anchorage</td>
            <td>AK</td>
            <td>500.0</td>
        </tr>
        <tr>
            <td>Mercyhealth Hospital Rockton Avenue</td>
            <td>Rockford</td>
            <td>IL</td>
            <td>501.0</td>
        </tr>
        <tr>
            <td>Hutchinson Health</td>
            <td>Hutchinson</td>
            <td>MN</td>
            <td>502.0</td>
        </tr>
        <tr>
            <td>Logan Health Medical Center</td>
            <td>Kalispell</td>
            <td>MT</td>
            <td>503.0</td>
        </tr>
        <tr>
            <td>Wooster Community Hospital</td>
            <td>Wooster</td>
            <td>OH</td>
            <td>504.0</td>
        </tr>
        <tr>
            <td>City Hospital AtÂ¬â€  White Rock</td>
            <td>Dallas</td>
            <td>TX</td>
            <td>505.0</td>
        </tr>
        <tr>
            <td>IU Health West Hospital</td>
            <td>Avon</td>
            <td>IN</td>
            <td>506.0</td>
        </tr>
        <tr>
            <td>Brigham and Women&#x27;s Faulkner Hospital</td>
            <td>Boston</td>
            <td>MA</td>
            <td>507.0</td>
        </tr>
        <tr>
            <td>Mercy Medical Center-Dubuque</td>
            <td>Dubuque</td>
            <td>IA</td>
            <td>508.0</td>
        </tr>
        <tr>
            <td>Barnes-Jewish St. Peters Hospital</td>
            <td>Saint Peters</td>
            <td>MO</td>
            <td>509.0</td>
        </tr>
        <tr>
            <td>Adventist Health Castle</td>
            <td>Kailua</td>
            <td>HI</td>
            <td>510.0</td>
        </tr>
        <tr>
            <td>Saint Joseph East</td>
            <td>Lexington</td>
            <td>KY</td>
            <td>511.0</td>
        </tr>
        <tr>
            <td>Park Nicollet Methodist Hospital</td>
            <td>Saint Louis Park</td>
            <td>MN</td>
            <td>513.0</td>
        </tr>
        <tr>
            <td>Sanford Medical Center Bismarck</td>
            <td>Bismarck</td>
            <td>ND</td>
            <td>514.0</td>
        </tr>
        <tr>
            <td>Mercy Medical Center - Cedar Rapids</td>
            <td>Cedar Rapids</td>
            <td>IA</td>
            <td>515.0</td>
        </tr>
        <tr>
            <td>Inova Mount Vernon Hospital</td>
            <td>Alexandria</td>
            <td>VA</td>
            <td>516.0</td>
        </tr>
        <tr>
            <td>Ridgeview Medical Center</td>
            <td>Waconia</td>
            <td>MN</td>
            <td>517.0</td>
        </tr>
        <tr>
            <td>Tristar Centennial Medical Center</td>
            <td>Nashville</td>
            <td>TN</td>
            <td>518.0</td>
        </tr>
        <tr>
            <td>Metro Health Hospital</td>
            <td>Wyoming</td>
            <td>MI</td>
            <td>519.0</td>
        </tr>
        <tr>
            <td>Waynesboro Hospital</td>
            <td>Waynesboro</td>
            <td>PA</td>
            <td>520.0</td>
        </tr>
        <tr>
            <td>Advocate Condell Medical Center</td>
            <td>Libertyville</td>
            <td>IL</td>
            <td>521.0</td>
        </tr>
        <tr>
            <td>Ascension St. Clares Hospital</td>
            <td>Weston</td>
            <td>WI</td>
            <td>522.0</td>
        </tr>
        <tr>
            <td>Monroe Hospital</td>
            <td>Bloomington</td>
            <td>IN</td>
            <td>523.0</td>
        </tr>
        <tr>
            <td>The Moses H. Cone Memorial Hospital</td>
            <td>Greensboro</td>
            <td>NC</td>
            <td>524.0</td>
        </tr>
        <tr>
            <td>Lake Region Healthcare</td>
            <td>Fergus Falls</td>
            <td>MN</td>
            <td>525.0</td>
        </tr>
        <tr>
            <td>Plaza Medical Center of Fort Worth</td>
            <td>Fort Worth</td>
            <td>TX</td>
            <td>526.0</td>
        </tr>
        <tr>
            <td>Grand Strand Regional Medical Center</td>
            <td>Myrtle Beach</td>
            <td>SC</td>
            <td>527.0</td>
        </tr>
        <tr>
            <td>Ascension SE Wisconsin Hospital - St. Joseph Campus</td>
            <td>Milwaukee</td>
            <td>WI</td>
            <td>528.0</td>
        </tr>
        <tr>
            <td>United Hospital</td>
            <td>Saint Paul</td>
            <td>MN</td>
            <td>529.0</td>
        </tr>
        <tr>
            <td>Sutter Santa Rosa Regional Hospital</td>
            <td>Santa Rosa</td>
            <td>CA</td>
            <td>530.0</td>
        </tr>
        <tr>
            <td>Timpanogos Regional Hospital</td>
            <td>Orem</td>
            <td>UT</td>
            <td>531.0</td>
        </tr>
        <tr>
            <td>Chambersburg Hospital</td>
            <td>Chambersburg</td>
            <td>PA</td>
            <td>532.0</td>
        </tr>
        <tr>
            <td>West Chester Hospital</td>
            <td>West Chester</td>
            <td>OH</td>
            <td>533.0</td>
        </tr>
        <tr>
            <td>Margaret R Pardee Memorial Hospital</td>
            <td>Hendersonville</td>
            <td>NC</td>
            <td>534.0</td>
        </tr>
        <tr>
            <td>Community Hospital of the Monterey Peninsula</td>
            <td>Monterey</td>
            <td>CA</td>
            <td>535.0</td>
        </tr>
        <tr>
            <td>Baylor Scott &amp; White Medical Center - Round Rock</td>
            <td>Round Rock</td>
            <td>TX</td>
            <td>536.0</td>
        </tr>
        <tr>
            <td>Memorial Mission Hospital and Asheville Surgery Center</td>
            <td>Asheville</td>
            <td>NC</td>
            <td>537.0</td>
        </tr>
        <tr>
            <td>Novato Community Hospital</td>
            <td>Novato</td>
            <td>CA</td>
            <td>538.0</td>
        </tr>
        <tr>
            <td>CJW Medical Center</td>
            <td>Richmond</td>
            <td>VA</td>
            <td>539.0</td>
        </tr>
        <tr>
            <td>Carolinas Healthcare System Northeast</td>
            <td>Concord</td>
            <td>NC</td>
            <td>540.0</td>
        </tr>
        <tr>
            <td>McLaren Central Michigan</td>
            <td>Mount Pleasant</td>
            <td>MI</td>
            <td>541.0</td>
        </tr>
        <tr>
            <td>Essentia Health St. Marys - Detroit Lakes</td>
            <td>Detroit Lakes</td>
            <td>MN</td>
            <td>542.0</td>
        </tr>
        <tr>
            <td>Christ Hospital</td>
            <td>Cincinnati</td>
            <td>OH</td>
            <td>543.0</td>
        </tr>
        <tr>
            <td>Adventist Health St. Helena</td>
            <td>Saint Helena</td>
            <td>CA</td>
            <td>544.0</td>
        </tr>
        <tr>
            <td>Kadlec Regional Medical Center</td>
            <td>Richland</td>
            <td>WA</td>
            <td>545.0</td>
        </tr>
        <tr>
            <td>Warren Memorial Hospital</td>
            <td>Front Royal</td>
            <td>VA</td>
            <td>546.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital</td>
            <td>Iowa City</td>
            <td>IA</td>
            <td>547.0</td>
        </tr>
        <tr>
            <td>Finley Hospital</td>
            <td>Dubuque</td>
            <td>IA</td>
            <td>548.0</td>
        </tr>
        <tr>
            <td>Lehigh Valley Hospital</td>
            <td>Allentown</td>
            <td>PA</td>
            <td>549.0</td>
        </tr>
        <tr>
            <td>Jewish Hospital</td>
            <td>Cincinnati</td>
            <td>OH</td>
            <td>550.0</td>
        </tr>
        <tr>
            <td>Methodist Medical Center of Illinois</td>
            <td>Peoria</td>
            <td>IL</td>
            <td>551.0</td>
        </tr>
        <tr>
            <td>Mount Sinai Hospital</td>
            <td>New York</td>
            <td>NY</td>
            <td>552.0</td>
        </tr>
        <tr>
            <td>Jordan Valley Medical Center</td>
            <td>West Jordan</td>
            <td>UT</td>
            <td>553.0</td>
        </tr>
        <tr>
            <td>Thomas Jefferson University Hospital</td>
            <td>Philadelphia</td>
            <td>PA</td>
            <td>554.0</td>
        </tr>
        <tr>
            <td>AdventHealth Gordon</td>
            <td>Calhoun</td>
            <td>GA</td>
            <td>555.0</td>
        </tr>
        <tr>
            <td>Lutheran Medical Center</td>
            <td>Wheat Ridge</td>
            <td>CO</td>
            <td>556.0</td>
        </tr>
        <tr>
            <td>Mosaic Life Care at St. Joseph</td>
            <td>Saint Joseph</td>
            <td>MO</td>
            <td>557.0</td>
        </tr>
        <tr>
            <td>Saratoga Hospital</td>
            <td>Saratoga Springs</td>
            <td>NY</td>
            <td>558.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Fairfield</td>
            <td>Fairfield</td>
            <td>OH</td>
            <td>559.0</td>
        </tr>
        <tr>
            <td>Sutter Roseville Medical Center</td>
            <td>Roseville</td>
            <td>CA</td>
            <td>560.0</td>
        </tr>
        <tr>
            <td>Cleveland Clinic</td>
            <td>Cleveland</td>
            <td>OH</td>
            <td>562.0</td>
        </tr>
        <tr>
            <td>Bronson Methodist Hospital</td>
            <td>Kalamazoo</td>
            <td>MI</td>
            <td>563.0</td>
        </tr>
        <tr>
            <td>Essentia Health Fargo</td>
            <td>Fargo</td>
            <td>ND</td>
            <td>564.0</td>
        </tr>
        <tr>
            <td>Allegheny Valley Hospital</td>
            <td>Natrona</td>
            <td>PA</td>
            <td>565.0</td>
        </tr>
        <tr>
            <td>Munson Medical Center</td>
            <td>Traverse City</td>
            <td>MI</td>
            <td>566.0</td>
        </tr>
        <tr>
            <td>Central Florida Regional Hospital</td>
            <td>Sanford</td>
            <td>FL</td>
            <td>567.0</td>
        </tr>
        <tr>
            <td>Centura Health-Porter Adventist Hospital</td>
            <td>Denver</td>
            <td>CO</td>
            <td>568.0</td>
        </tr>
        <tr>
            <td>Centura Health-Avista Adventist Hospital</td>
            <td>Louisville</td>
            <td>CO</td>
            <td>569.0</td>
        </tr>
        <tr>
            <td>Medical City Alliance</td>
            <td>Fort Worth</td>
            <td>TX</td>
            <td>570.0</td>
        </tr>
        <tr>
            <td>Christus St. Vincent Regional Medical Center</td>
            <td>Santa Fe</td>
            <td>NM</td>
            <td>571.0</td>
        </tr>
        <tr>
            <td>Pinnacle Health Hospitals</td>
            <td>Harrisburg</td>
            <td>PA</td>
            <td>572.0</td>
        </tr>
        <tr>
            <td>Mercy Health St. Vincent Medical Center</td>
            <td>Toledo</td>
            <td>OH</td>
            <td>573.0</td>
        </tr>
        <tr>
            <td>Sanford USD Medical Center</td>
            <td>Sioux Falls</td>
            <td>SD</td>
            <td>574.0</td>
        </tr>
        <tr>
            <td>Delta County Memorial Hospital</td>
            <td>Delta</td>
            <td>CO</td>
            <td>575.0</td>
        </tr>
        <tr>
            <td>Northwestern Medicine Mchenry Hospital</td>
            <td>McHenry</td>
            <td>IL</td>
            <td>576.0</td>
        </tr>
        <tr>
            <td>Fairview Southdale Hospital</td>
            <td>Edina</td>
            <td>MN</td>
            <td>577.0</td>
        </tr>
        <tr>
            <td>Hendrick Medical Center</td>
            <td>Abilene</td>
            <td>TX</td>
            <td>578.0</td>
        </tr>
        <tr>
            <td>HCA Houston Healthcare Clear Lake</td>
            <td>Webster</td>
            <td>TX</td>
            <td>579.0</td>
        </tr>
        <tr>
            <td>Saint Joseph Regional Medical Center</td>
            <td>Mishawaka</td>
            <td>IN</td>
            <td>580.0</td>
        </tr>
        <tr>
            <td>Chi Health St. Elizabeth</td>
            <td>Lincoln</td>
            <td>NE</td>
            <td>581.0</td>
        </tr>
        <tr>
            <td>Holland Community Hospital</td>
            <td>Holland</td>
            <td>MI</td>
            <td>582.0</td>
        </tr>
        <tr>
            <td>Mercy Medical Center-North Iowa</td>
            <td>Mason City</td>
            <td>IA</td>
            <td>583.0</td>
        </tr>
        <tr>
            <td>Centura Health-St. Anthony Hospital</td>
            <td>Lakewood</td>
            <td>CO</td>
            <td>584.0</td>
        </tr>
        <tr>
            <td>Hays Medical Center</td>
            <td>Hays</td>
            <td>KS</td>
            <td>585.0</td>
        </tr>
        <tr>
            <td>Northern Nevada Medical Center</td>
            <td>Sparks</td>
            <td>NV</td>
            <td>586.0</td>
        </tr>
        <tr>
            <td>The Toledo Hospital</td>
            <td>Toledo</td>
            <td>OH</td>
            <td>587.0</td>
        </tr>
        <tr>
            <td>St. Joseph Mercy Hospital</td>
            <td>Ann Arbor</td>
            <td>MI</td>
            <td>588.0</td>
        </tr>
        <tr>
            <td>Avera Mckennan Hospital &amp; University Health Center</td>
            <td>Sioux Falls</td>
            <td>SD</td>
            <td>589.0</td>
        </tr>
        <tr>
            <td>Hudson Hospital &amp; Clinic</td>
            <td>Hudson</td>
            <td>WI</td>
            <td>590.0</td>
        </tr>
        <tr>
            <td>Froedtert Hospital</td>
            <td>Milwaukee</td>
            <td>WI</td>
            <td>591.0</td>
        </tr>
        <tr>
            <td>Reading Hospital</td>
            <td>Reading</td>
            <td>PA</td>
            <td>592.0</td>
        </tr>
        <tr>
            <td>Central Texas Medical Center</td>
            <td>San Marcos</td>
            <td>TX</td>
            <td>593.0</td>
        </tr>
        <tr>
            <td>Spectrum Health Zeeland Community Hospital</td>
            <td>Zeeland</td>
            <td>MI</td>
            <td>594.0</td>
        </tr>
        <tr>
            <td>Powell Valley Hospital</td>
            <td>Powell</td>
            <td>WY</td>
            <td>595.0</td>
        </tr>
        <tr>
            <td>Cartersville Medical Center</td>
            <td>Cartersville</td>
            <td>GA</td>
            <td>596.0</td>
        </tr>
        <tr>
            <td>Lakeview Hospital</td>
            <td>Bountiful</td>
            <td>UT</td>
            <td>597.0</td>
        </tr>
        <tr>
            <td>Elmhurst Memorial Hospital</td>
            <td>Elmhurst</td>
            <td>IL</td>
            <td>598.0</td>
        </tr>
        <tr>
            <td>Perry Hospital</td>
            <td>Perry</td>
            <td>GA</td>
            <td>599.0</td>
        </tr>
        <tr>
            <td>Mercy Health Muskegon</td>
            <td>Muskegon</td>
            <td>MI</td>
            <td>600.0</td>
        </tr>
        <tr>
            <td>Duke University Hospital</td>
            <td>Durham</td>
            <td>NC</td>
            <td>601.0</td>
        </tr>
        <tr>
            <td>Baptist Health Medical Center Heber Spings</td>
            <td>Heber Springs</td>
            <td>AR</td>
            <td>602.0</td>
        </tr>
        <tr>
            <td>St. Nicholas Hospital</td>
            <td>Sheboygan</td>
            <td>WI</td>
            <td>603.0</td>
        </tr>
        <tr>
            <td>Mercy Medical Center-Des Moines</td>
            <td>Des Moines</td>
            <td>IA</td>
            <td>604.0</td>
        </tr>
        <tr>
            <td>Riverside Methodist Hospital</td>
            <td>Columbus</td>
            <td>OH</td>
            <td>605.0</td>
        </tr>
        <tr>
            <td>Chi St. Alexius Health</td>
            <td>Bismarck</td>
            <td>ND</td>
            <td>606.0</td>
        </tr>
        <tr>
            <td>Coliseum Medical Centers</td>
            <td>Macon</td>
            <td>GA</td>
            <td>607.0</td>
        </tr>
        <tr>
            <td>Sanford Canton-Inwood Medical Center - Cah</td>
            <td>Canton</td>
            <td>SD</td>
            <td>608.0</td>
        </tr>
        <tr>
            <td>Memorial Healthcare System</td>
            <td>Chattanooga</td>
            <td>TN</td>
            <td>609.0</td>
        </tr>
        <tr>
            <td>St. Elizabeth Hospital</td>
            <td>Enumclaw</td>
            <td>WA</td>
            <td>610.0</td>
        </tr>
        <tr>
            <td>Northside Hospital Forsyth</td>
            <td>Cumming</td>
            <td>GA</td>
            <td>611.0</td>
        </tr>
        <tr>
            <td>Prisma Health Greer Memorial Hospital</td>
            <td>Greer</td>
            <td>SC</td>
            <td>612.0</td>
        </tr>
        <tr>
            <td>Baptist Hospital</td>
            <td>Pensacola</td>
            <td>FL</td>
            <td>613.0</td>
        </tr>
        <tr>
            <td>Providence Holy Family Hospital</td>
            <td>Spokane</td>
            <td>WA</td>
            <td>614.0</td>
        </tr>
        <tr>
            <td>Michigan Medicine</td>
            <td>Ann Arbor</td>
            <td>MI</td>
            <td>615.0</td>
        </tr>
        <tr>
            <td>Saint Joseph Mount Sterling</td>
            <td>Mount Sterling</td>
            <td>KY</td>
            <td>616.0</td>
        </tr>
        <tr>
            <td>Providence Kodiak Island Medical Center</td>
            <td>Kodiak</td>
            <td>AK</td>
            <td>617.0</td>
        </tr>
        <tr>
            <td>St. Vincent Anderson Regional Hospital</td>
            <td>Anderson</td>
            <td>IN</td>
            <td>618.0</td>
        </tr>
        <tr>
            <td>New York-Presbyterian Brooklyn Methodist Hospital</td>
            <td>Brooklyn</td>
            <td>NY</td>
            <td>619.0</td>
        </tr>
        <tr>
            <td>Huntington Hospital</td>
            <td>Huntington</td>
            <td>NY</td>
            <td>622.0</td>
        </tr>
        <tr>
            <td>Northwest Texas Hospital</td>
            <td>Amarillo</td>
            <td>TX</td>
            <td>623.0</td>
        </tr>
        <tr>
            <td>Saint Francis Hospital</td>
            <td>Tulsa</td>
            <td>OK</td>
            <td>624.0</td>
        </tr>
        <tr>
            <td>Hospital of University of Pennsylvania</td>
            <td>Philadelphia</td>
            <td>PA</td>
            <td>625.0</td>
        </tr>
        <tr>
            <td>The University of Tennessee Medical Center</td>
            <td>Knoxville</td>
            <td>TN</td>
            <td>626.0</td>
        </tr>
        <tr>
            <td>Winchester Hospital</td>
            <td>Winchester</td>
            <td>MA</td>
            <td>627.0</td>
        </tr>
        <tr>
            <td>Naples Community Hospital</td>
            <td>Naples</td>
            <td>FL</td>
            <td>628.0</td>
        </tr>
        <tr>
            <td>Gulf Coast Regional Medical Center</td>
            <td>Panama City</td>
            <td>FL</td>
            <td>629.0</td>
        </tr>
        <tr>
            <td>Saline Memorial Hospital</td>
            <td>Benton</td>
            <td>AR</td>
            <td>630.0</td>
        </tr>
        <tr>
            <td>Heritage Valley Sewickley</td>
            <td>Sewickley</td>
            <td>PA</td>
            <td>631.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Regional Medical Center</td>
            <td>Boise</td>
            <td>ID</td>
            <td>632.0</td>
        </tr>
        <tr>
            <td>French Hospital Medical Center</td>
            <td>San Luis Obispo</td>
            <td>CA</td>
            <td>633.0</td>
        </tr>
        <tr>
            <td>Avera St. Luke&#x27;s</td>
            <td>Aberdeen</td>
            <td>SD</td>
            <td>634.0</td>
        </tr>
        <tr>
            <td>Parker Adventist Hospital</td>
            <td>Parker</td>
            <td>CO</td>
            <td>635.0</td>
        </tr>
        <tr>
            <td>Providence - Providence Park Hospital</td>
            <td>Southfield</td>
            <td>MI</td>
            <td>636.0</td>
        </tr>
        <tr>
            <td>Coliseum Northside Hospital</td>
            <td>Macon</td>
            <td>GA</td>
            <td>637.0</td>
        </tr>
        <tr>
            <td>Castle Rock Adventist Hospital</td>
            <td>Castle Rock</td>
            <td>CO</td>
            <td>638.0</td>
        </tr>
        <tr>
            <td>Massachusetts General Hospital</td>
            <td>Boston</td>
            <td>MA</td>
            <td>639.0</td>
        </tr>
        <tr>
            <td>FirstHealth Moore Regional Hospital</td>
            <td>Pinehurst</td>
            <td>NC</td>
            <td>640.0</td>
        </tr>
        <tr>
            <td>North Okaloosa Medical Center</td>
            <td>Crestview</td>
            <td>FL</td>
            <td>641.0</td>
        </tr>
        <tr>
            <td>Cape Fear Valley Hoke Hospital</td>
            <td>Raeford</td>
            <td>NC</td>
            <td>642.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Warren Hospital</td>
            <td>Phillipsburg</td>
            <td>NJ</td>
            <td>644.0</td>
        </tr>
        <tr>
            <td>Medical City Arlington</td>
            <td>Arlington</td>
            <td>TX</td>
            <td>645.0</td>
        </tr>
        <tr>
            <td>Southeast Georgia Health System - Camden Campus</td>
            <td>Saint Marys</td>
            <td>GA</td>
            <td>646.0</td>
        </tr>
        <tr>
            <td>Scripps Memorial Hospital - Encinitas</td>
            <td>Encinitas</td>
            <td>CA</td>
            <td>647.0</td>
        </tr>
        <tr>
            <td>Sierra Vista Regional Medical Center</td>
            <td>San Luis Obispo</td>
            <td>CA</td>
            <td>648.0</td>
        </tr>
        <tr>
            <td>Tampa General Hospital</td>
            <td>Tampa</td>
            <td>FL</td>
            <td>649.0</td>
        </tr>
        <tr>
            <td>Carilion New River Valley Medical Center</td>
            <td>Christiansburg</td>
            <td>VA</td>
            <td>650.0</td>
        </tr>
        <tr>
            <td>Mather Hospital</td>
            <td>Port Jefferson</td>
            <td>NY</td>
            <td>652.0</td>
        </tr>
        <tr>
            <td>Abbeville General Hospital</td>
            <td>Abbeville</td>
            <td>LA</td>
            <td>653.0</td>
        </tr>
        <tr>
            <td>Pomerado Hospital</td>
            <td>Poway</td>
            <td>CA</td>
            <td>654.0</td>
        </tr>
        <tr>
            <td>Orange Park Medical Center</td>
            <td>Orange Park</td>
            <td>FL</td>
            <td>655.0</td>
        </tr>
        <tr>
            <td>Mount Carmel St. Ann&#x27;s</td>
            <td>Westerville</td>
            <td>OH</td>
            <td>656.0</td>
        </tr>
        <tr>
            <td>Bellin Memorial Hospital</td>
            <td>Green Bay</td>
            <td>WI</td>
            <td>657.0</td>
        </tr>
        <tr>
            <td>Heart of Lancaster Medical Center</td>
            <td>Lititz</td>
            <td>PA</td>
            <td>658.0</td>
        </tr>
        <tr>
            <td>St. Joseph&#x27;s Hospital</td>
            <td>Saint Paul</td>
            <td>MN</td>
            <td>659.0</td>
        </tr>
        <tr>
            <td>Ascension St. Michaels Hospital</td>
            <td>Stevens Point</td>
            <td>WI</td>
            <td>660.0</td>
        </tr>
        <tr>
            <td>Bay Area Medical Center</td>
            <td>Marinette</td>
            <td>WI</td>
            <td>661.0</td>
        </tr>
        <tr>
            <td>Iowa Methodist Medical Center</td>
            <td>Des Moines</td>
            <td>IA</td>
            <td>662.0</td>
        </tr>
        <tr>
            <td>Kootenai Health</td>
            <td>Coeur D&#x27;Alene</td>
            <td>ID</td>
            <td>663.0</td>
        </tr>
        <tr>
            <td>Vanderbilt University Medical Center</td>
            <td>Nashville</td>
            <td>TN</td>
            <td>664.0</td>
        </tr>
        <tr>
            <td>Einstein Medical Center Montgomery</td>
            <td>East Norriton</td>
            <td>PA</td>
            <td>665.0</td>
        </tr>
        <tr>
            <td>Stanford Health Care - Valleycare</td>
            <td>Pleasanton</td>
            <td>CA</td>
            <td>666.0</td>
        </tr>
        <tr>
            <td>Sharp Memorial Hospital</td>
            <td>San Diego</td>
            <td>CA</td>
            <td>667.0</td>
        </tr>
        <tr>
            <td>Exeter Hospital</td>
            <td>Exeter</td>
            <td>NH</td>
            <td>668.0</td>
        </tr>
        <tr>
            <td>Loyola Gottlieb Memorial Hospital</td>
            <td>Melrose Park</td>
            <td>IL</td>
            <td>669.0</td>
        </tr>
        <tr>
            <td>Laredo Medical Center</td>
            <td>Laredo</td>
            <td>TX</td>
            <td>670.0</td>
        </tr>
        <tr>
            <td>Edward W. Sparrow Hospital</td>
            <td>Lansing</td>
            <td>MI</td>
            <td>671.0</td>
        </tr>
        <tr>
            <td>Georgetown Community Hospital</td>
            <td>Georgetown</td>
            <td>KY</td>
            <td>672.0</td>
        </tr>
        <tr>
            <td>Piedmont Hospital</td>
            <td>Atlanta</td>
            <td>GA</td>
            <td>673.0</td>
        </tr>
        <tr>
            <td>Madison Memorial Hospital</td>
            <td>Rexburg</td>
            <td>ID</td>
            <td>674.0</td>
        </tr>
        <tr>
            <td>UNC Health Blue Ridge</td>
            <td>Morganton</td>
            <td>NC</td>
            <td>675.0</td>
        </tr>
        <tr>
            <td>Methodist Fremont Health</td>
            <td>Fremont</td>
            <td>NE</td>
            <td>676.0</td>
        </tr>
        <tr>
            <td>North Kansas City Hospital</td>
            <td>North Kansas City</td>
            <td>MO</td>
            <td>677.0</td>
        </tr>
        <tr>
            <td>Sutter Davis Hospital</td>
            <td>Davis</td>
            <td>CA</td>
            <td>678.0</td>
        </tr>
        <tr>
            <td>Parkview Regional Medical Center</td>
            <td>Fort Wayne</td>
            <td>IN</td>
            <td>679.0</td>
        </tr>
        <tr>
            <td>Deaconess Hospital</td>
            <td>Evansville</td>
            <td>IN</td>
            <td>680.0</td>
        </tr>
        <tr>
            <td>St. Lukes Hospital of Kansas City</td>
            <td>Kansas City</td>
            <td>MO</td>
            <td>681.0</td>
        </tr>
        <tr>
            <td>St. Vincent&#x27;s Medical Center Riverside</td>
            <td>Jacksonville</td>
            <td>FL</td>
            <td>682.0</td>
        </tr>
        <tr>
            <td>Platte County Memorial Hospital</td>
            <td>Wheatland</td>
            <td>WY</td>
            <td>683.0</td>
        </tr>
        <tr>
            <td>Texas Health Huguley Hospital Fort Worth South</td>
            <td>Burleson</td>
            <td>TX</td>
            <td>684.0</td>
        </tr>
        <tr>
            <td>Mountainview Hospital</td>
            <td>Las Vegas</td>
            <td>NV</td>
            <td>685.0</td>
        </tr>
        <tr>
            <td>Presence St. Mary&#x27;s Hospital</td>
            <td>Kankakee</td>
            <td>IL</td>
            <td>686.0</td>
        </tr>
        <tr>
            <td>Valley View</td>
            <td>Glenwood Springs</td>
            <td>CO</td>
            <td>687.0</td>
        </tr>
        <tr>
            <td>Nacogdoches Medical Center</td>
            <td>Nacogdoches</td>
            <td>TX</td>
            <td>688.0</td>
        </tr>
        <tr>
            <td>AdventHealth Zephyrhills</td>
            <td>Zephyrhills</td>
            <td>FL</td>
            <td>689.0</td>
        </tr>
        <tr>
            <td>Christiana Care Health Services</td>
            <td>Newark</td>
            <td>DE</td>
            <td>690.0</td>
        </tr>
        <tr>
            <td>Baylor Scott and White All Saints Medical Center</td>
            <td>Fort Worth</td>
            <td>TX</td>
            <td>691.0</td>
        </tr>
        <tr>
            <td>West Penn Hospital</td>
            <td>Pittsburgh</td>
            <td>PA</td>
            <td>692.0</td>
        </tr>
        <tr>
            <td>Kent County Memorial Hospital</td>
            <td>Warwick</td>
            <td>RI</td>
            <td>693.0</td>
        </tr>
        <tr>
            <td>Piedmont Fayette Hospital</td>
            <td>Fayetteville</td>
            <td>GA</td>
            <td>694.0</td>
        </tr>
        <tr>
            <td>CHI St. Luke&#x27;s Health Baylor College of Medicine</td>
            <td>Houston</td>
            <td>TX</td>
            <td>695.0</td>
        </tr>
        <tr>
            <td>Northwest Community Hospital</td>
            <td>Arlington Heights</td>
            <td>IL</td>
            <td>696.0</td>
        </tr>
        <tr>
            <td>Mease Dunedin Hospital</td>
            <td>Dunedin</td>
            <td>FL</td>
            <td>697.0</td>
        </tr>
        <tr>
            <td>Banner Ironwood Medical Center</td>
            <td>Queen Creek</td>
            <td>AZ</td>
            <td>698.0</td>
        </tr>
        <tr>
            <td>Yale-New Haven Hospital</td>
            <td>New Haven</td>
            <td>CT</td>
            <td>700.0</td>
        </tr>
        <tr>
            <td>Mcleod LorisÂ¬â€ Hospital</td>
            <td>Loris</td>
            <td>SC</td>
            <td>701.0</td>
        </tr>
        <tr>
            <td>Berkeley Medical Center</td>
            <td>Martinsburg</td>
            <td>WV</td>
            <td>702.0</td>
        </tr>
        <tr>
            <td>Banner Gateway Medical Center</td>
            <td>Gilbert</td>
            <td>AZ</td>
            <td>703.0</td>
        </tr>
        <tr>
            <td>Memorial Hermann Hospital System</td>
            <td>Houston</td>
            <td>TX</td>
            <td>704.0</td>
        </tr>
        <tr>
            <td>Palomar Health Downtown Campus</td>
            <td>Escondido</td>
            <td>CA</td>
            <td>705.0</td>
        </tr>
        <tr>
            <td>Alta Bates Summit Medical Center - Alta Bates Camp</td>
            <td>Berkeley</td>
            <td>CA</td>
            <td>706.0</td>
        </tr>
        <tr>
            <td>Mount Pleasant Hospital</td>
            <td>Mount Pleasant</td>
            <td>SC</td>
            <td>707.0</td>
        </tr>
        <tr>
            <td>Wakemed</td>
            <td>Cary</td>
            <td>NC</td>
            <td>708.0</td>
        </tr>
        <tr>
            <td>Orlando Health Orlando Regional Medical Center</td>
            <td>Orlando</td>
            <td>FL</td>
            <td>709.0</td>
        </tr>
        <tr>
            <td>Chesapeake General Hospital</td>
            <td>Chesapeake</td>
            <td>VA</td>
            <td>710.0</td>
        </tr>
        <tr>
            <td>Shawnee Mission Medical Center</td>
            <td>Shawnee Mission</td>
            <td>KS</td>
            <td>712.0</td>
        </tr>
        <tr>
            <td>St. Agnes Hospital</td>
            <td>Fond Du Lac</td>
            <td>WI</td>
            <td>713.0</td>
        </tr>
        <tr>
            <td>Riverside Doctors&#x27; Hospital of Williamsburg</td>
            <td>Williamsburg</td>
            <td>VA</td>
            <td>714.0</td>
        </tr>
        <tr>
            <td>Scott &amp; White Hospital Brenham</td>
            <td>Brenham</td>
            <td>TX</td>
            <td>715.0</td>
        </tr>
        <tr>
            <td>Inova Fairfax Hospital</td>
            <td>Falls Church</td>
            <td>VA</td>
            <td>717.0</td>
        </tr>
        <tr>
            <td>St. Marys Hospital Medical Center</td>
            <td>Green Bay</td>
            <td>WI</td>
            <td>719.0</td>
        </tr>
        <tr>
            <td>Advocate Christ Hospital &amp; Medical Center</td>
            <td>Oak Lawn</td>
            <td>IL</td>
            <td>720.0</td>
        </tr>
        <tr>
            <td>Saint Thomas River Park Hospital</td>
            <td>McMinnville</td>
            <td>TN</td>
            <td>721.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Sugar Land Hospital</td>
            <td>Sugar Land</td>
            <td>TX</td>
            <td>722.0</td>
        </tr>
        <tr>
            <td>Encino Hospital Medical Center</td>
            <td>Encino</td>
            <td>CA</td>
            <td>723.0</td>
        </tr>
        <tr>
            <td>Northridge Hospital Medical Center</td>
            <td>Northridge</td>
            <td>CA</td>
            <td>724.0</td>
        </tr>
        <tr>
            <td>Chestnut Hill Hospital</td>
            <td>Philadelphia</td>
            <td>PA</td>
            <td>726.0</td>
        </tr>
        <tr>
            <td>Alomere Health</td>
            <td>Alexandria</td>
            <td>MN</td>
            <td>727.0</td>
        </tr>
        <tr>
            <td>IU Health Bloomington Hospital</td>
            <td>Bloomington</td>
            <td>IN</td>
            <td>728.0</td>
        </tr>
        <tr>
            <td>UP Health System - Marquette</td>
            <td>Marquette</td>
            <td>MI</td>
            <td>729.0</td>
        </tr>
        <tr>
            <td>Ashley Regional Medical Center</td>
            <td>Vernal</td>
            <td>UT</td>
            <td>730.0</td>
        </tr>
        <tr>
            <td>Santa Rosa Memorial Hospital</td>
            <td>Santa Rosa</td>
            <td>CA</td>
            <td>731.0</td>
        </tr>
        <tr>
            <td>Ascension Via Christi Hospital Manhattan</td>
            <td>Manhattan</td>
            <td>KS</td>
            <td>732.0</td>
        </tr>
        <tr>
            <td>Texas Health Southwest Fort Worth</td>
            <td>Fort Worth</td>
            <td>TX</td>
            <td>733.0</td>
        </tr>
        <tr>
            <td>Mercy St. Charles Hospital</td>
            <td>Oregon</td>
            <td>OH</td>
            <td>734.0</td>
        </tr>
        <tr>
            <td>St. Vincent Hospital</td>
            <td>Worcester</td>
            <td>MA</td>
            <td>735.0</td>
        </tr>
        <tr>
            <td>New York-Presbyterian/Queens</td>
            <td>Flushing</td>
            <td>NY</td>
            <td>736.0</td>
        </tr>
        <tr>
            <td>Wellstar Kennestone Hospital</td>
            <td>Marietta</td>
            <td>GA</td>
            <td>737.0</td>
        </tr>
        <tr>
            <td>AdventHealth North Pinellas</td>
            <td>Tarpon Springs</td>
            <td>FL</td>
            <td>738.0</td>
        </tr>
        <tr>
            <td>Ogden Regional Medical Center</td>
            <td>Ogden</td>
            <td>UT</td>
            <td>739.0</td>
        </tr>
        <tr>
            <td>The Corpus Christi Medical Center</td>
            <td>Corpus Christi</td>
            <td>TX</td>
            <td>740.0</td>
        </tr>
        <tr>
            <td>Glen Cove Hospital</td>
            <td>Glen Cove</td>
            <td>NY</td>
            <td>741.0</td>
        </tr>
        <tr>
            <td>Walker Baptist Medical Center</td>
            <td>Jasper</td>
            <td>AL</td>
            <td>742.0</td>
        </tr>
        <tr>
            <td>UPMC St. Margaret</td>
            <td>Pittsburgh</td>
            <td>PA</td>
            <td>743.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Health - Patients Medical Center</td>
            <td>Pasadena</td>
            <td>TX</td>
            <td>744.0</td>
        </tr>
        <tr>
            <td>Caldwell Memorial Hospital</td>
            <td>Lenoir</td>
            <td>NC</td>
            <td>745.0</td>
        </tr>
        <tr>
            <td>Norman Regional</td>
            <td>Norman</td>
            <td>OK</td>
            <td>746.0</td>
        </tr>
        <tr>
            <td>Rush Oak Park Hospital</td>
            <td>Oak Park</td>
            <td>IL</td>
            <td>747.0</td>
        </tr>
        <tr>
            <td>Lee&#x27;s Summit Medical Center</td>
            <td>Lees Summit</td>
            <td>MO</td>
            <td>748.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Anderson</td>
            <td>Cincinnati</td>
            <td>OH</td>
            <td>749.0</td>
        </tr>
        <tr>
            <td>Mount Auburn Hospital</td>
            <td>Cambridge</td>
            <td>MA</td>
            <td>750.0</td>
        </tr>
        <tr>
            <td>SSM Health St. Mary&#x27;s Hospital -Centralia</td>
            <td>Centralia</td>
            <td>IL</td>
            <td>751.0</td>
        </tr>
        <tr>
            <td>Mercy Gilbert Medical Center</td>
            <td>Gilbert</td>
            <td>AZ</td>
            <td>752.0</td>
        </tr>
        <tr>
            <td>North Florida Regional Medical Center</td>
            <td>Gainesville</td>
            <td>FL</td>
            <td>753.0</td>
        </tr>
        <tr>
            <td>Saint Luke&#x27;s East Hospital</td>
            <td>Lees Summit</td>
            <td>MO</td>
            <td>754.0</td>
        </tr>
        <tr>
            <td>St. Francis Community Hospital</td>
            <td>Federal Way</td>
            <td>WA</td>
            <td>755.0</td>
        </tr>
        <tr>
            <td>Sentara Virginia Beach General Hospital</td>
            <td>Virginia Beach</td>
            <td>VA</td>
            <td>756.0</td>
        </tr>
        <tr>
            <td>Sutter Coast Hospital</td>
            <td>Crescent City</td>
            <td>CA</td>
            <td>758.0</td>
        </tr>
        <tr>
            <td>Mat-Su Regional Medical Center</td>
            <td>Palmer</td>
            <td>AK</td>
            <td>759.0</td>
        </tr>
        <tr>
            <td>Cedar Park Regional Medical Center</td>
            <td>Cedar Park</td>
            <td>TX</td>
            <td>760.0</td>
        </tr>
        <tr>
            <td>Mercy St. Anne Hospital</td>
            <td>Toledo</td>
            <td>OH</td>
            <td>761.0</td>
        </tr>
        <tr>
            <td>Mercy Health - Springfield Regional Medical Center</td>
            <td>Springfield</td>
            <td>OH</td>
            <td>762.0</td>
        </tr>
        <tr>
            <td>John Muir Medical Center - Concord Campus</td>
            <td>Concord</td>
            <td>CA</td>
            <td>763.0</td>
        </tr>
        <tr>
            <td>Bethesda North</td>
            <td>Cincinnati</td>
            <td>OH</td>
            <td>764.0</td>
        </tr>
        <tr>
            <td>Bay Medical Center Sacred Heart Health System</td>
            <td>Panama City</td>
            <td>FL</td>
            <td>765.0</td>
        </tr>
        <tr>
            <td>University of Maryland St. Joseph Medical Center</td>
            <td>Towson</td>
            <td>MD</td>
            <td>766.0</td>
        </tr>
        <tr>
            <td>Alexian Brothers Medical Center</td>
            <td>Elk Grove Village</td>
            <td>IL</td>
            <td>767.0</td>
        </tr>
        <tr>
            <td>Holy Spirit Hospital</td>
            <td>Camp Hill</td>
            <td>PA</td>
            <td>768.0</td>
        </tr>
        <tr>
            <td>Holmes Regional Medical Center</td>
            <td>Melbourne</td>
            <td>FL</td>
            <td>769.0</td>
        </tr>
        <tr>
            <td>Northbay Medical Center</td>
            <td>Fairfield</td>
            <td>CA</td>
            <td>770.0</td>
        </tr>
        <tr>
            <td>Flagler Hospital</td>
            <td>Saint Augustine</td>
            <td>FL</td>
            <td>771.0</td>
        </tr>
        <tr>
            <td>Christus Mother Frances Hospital Sulphur Springs</td>
            <td>Sulphur Springs</td>
            <td>TX</td>
            <td>772.0</td>
        </tr>
        <tr>
            <td>Indian Path Community Hospital</td>
            <td>Kingsport</td>
            <td>TN</td>
            <td>773.0</td>
        </tr>
        <tr>
            <td>Doctors&#x27;Â¬â€  Community Hospital</td>
            <td>Lanham</td>
            <td>MD</td>
            <td>774.0</td>
        </tr>
        <tr>
            <td>Lexington Medical Center</td>
            <td>West Columbia</td>
            <td>SC</td>
            <td>775.0</td>
        </tr>
        <tr>
            <td>Banner Desert Medical Center</td>
            <td>Mesa</td>
            <td>AZ</td>
            <td>776.0</td>
        </tr>
        <tr>
            <td>Medstar Montgomery Medical Center</td>
            <td>Olney</td>
            <td>MD</td>
            <td>777.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Ardmore</td>
            <td>Ardmore</td>
            <td>OK</td>
            <td>778.0</td>
        </tr>
        <tr>
            <td>Lower Bucks Hospital</td>
            <td>Bristol</td>
            <td>PA</td>
            <td>779.0</td>
        </tr>
        <tr>
            <td>Brownwood Regional Medical Center</td>
            <td>Brownwood</td>
            <td>TX</td>
            <td>781.0</td>
        </tr>
        <tr>
            <td>New Hanover Regional Medical Center</td>
            <td>Wilmington</td>
            <td>NC</td>
            <td>782.0</td>
        </tr>
        <tr>
            <td>Palms of Pasadena Hospital</td>
            <td>Saint Petersburg</td>
            <td>FL</td>
            <td>783.0</td>
        </tr>
        <tr>
            <td>Adventist Health Sonora</td>
            <td>Sonora</td>
            <td>CA</td>
            <td>784.0</td>
        </tr>
        <tr>
            <td>Christus Mother Frances Hospital</td>
            <td>Tyler</td>
            <td>TX</td>
            <td>785.0</td>
        </tr>
        <tr>
            <td>Ochsner Medical Center - Northshore</td>
            <td>Slidell</td>
            <td>LA</td>
            <td>786.0</td>
        </tr>
        <tr>
            <td>Lewisgale Hospital Montgomery</td>
            <td>Blacksburg</td>
            <td>VA</td>
            <td>787.0</td>
        </tr>
        <tr>
            <td>Wellstar North Fulton Hospital</td>
            <td>Roswell</td>
            <td>GA</td>
            <td>788.0</td>
        </tr>
        <tr>
            <td>Blessing Hospital</td>
            <td>Quincy</td>
            <td>IL</td>
            <td>789.0</td>
        </tr>
        <tr>
            <td>Brookwood Baptist Medical Center</td>
            <td>Birmingham</td>
            <td>AL</td>
            <td>790.0</td>
        </tr>
        <tr>
            <td>Southern Tennessee Regional Hlth System Winchester</td>
            <td>Winchester</td>
            <td>TN</td>
            <td>791.0</td>
        </tr>
        <tr>
            <td>Yavapai Regional Medical Center</td>
            <td>Prescott</td>
            <td>AZ</td>
            <td>792.0</td>
        </tr>
        <tr>
            <td>Kona Community Hospital</td>
            <td>Kealakekua</td>
            <td>HI</td>
            <td>794.0</td>
        </tr>
        <tr>
            <td>Advocate Lutheran General Hospital</td>
            <td>Park Ridge</td>
            <td>IL</td>
            <td>795.0</td>
        </tr>
        <tr>
            <td>Southwest General Health Center</td>
            <td>Middleburg Heights</td>
            <td>OH</td>
            <td>796.0</td>
        </tr>
        <tr>
            <td>Lehigh Regional Medical Center</td>
            <td>Lehigh Acres</td>
            <td>FL</td>
            <td>797.0</td>
        </tr>
        <tr>
            <td>UH Geauga Medical Center</td>
            <td>Chardon</td>
            <td>OH</td>
            <td>798.0</td>
        </tr>
        <tr>
            <td>Medical Center of Plano</td>
            <td>Plano</td>
            <td>TX</td>
            <td>799.0</td>
        </tr>
        <tr>
            <td>St. Mary Mercy Hospital</td>
            <td>Livonia</td>
            <td>MI</td>
            <td>800.0</td>
        </tr>
        <tr>
            <td>CHI St. Lukes Health Memorial Lufkin</td>
            <td>Lufkin</td>
            <td>TX</td>
            <td>801.0</td>
        </tr>
        <tr>
            <td>St. Vincents Medical Center - Clay County</td>
            <td>Middleburg</td>
            <td>FL</td>
            <td>802.0</td>
        </tr>
        <tr>
            <td>Queen of the Valley Medical Center</td>
            <td>Napa</td>
            <td>CA</td>
            <td>803.0</td>
        </tr>
        <tr>
            <td>Saint Vincent Hospital</td>
            <td>Erie</td>
            <td>PA</td>
            <td>804.0</td>
        </tr>
        <tr>
            <td>Frye Regional Medical Center</td>
            <td>Hickory</td>
            <td>NC</td>
            <td>805.0</td>
        </tr>
        <tr>
            <td>Indiana University Health North Hospital</td>
            <td>Carmel</td>
            <td>IN</td>
            <td>806.0</td>
        </tr>
        <tr>
            <td>Middlesex Hospital</td>
            <td>Middletown</td>
            <td>CT</td>
            <td>807.0</td>
        </tr>
        <tr>
            <td>Central Dupage Hospital</td>
            <td>Winfield</td>
            <td>IL</td>
            <td>808.0</td>
        </tr>
        <tr>
            <td>Orlando Health South Lake Hospital</td>
            <td>Clermont</td>
            <td>FL</td>
            <td>809.0</td>
        </tr>
        <tr>
            <td>Ascension St. Vincent Carmel</td>
            <td>Carmel</td>
            <td>IN</td>
            <td>810.0</td>
        </tr>
        <tr>
            <td>Medina Hospital</td>
            <td>Medina</td>
            <td>OH</td>
            <td>811.0</td>
        </tr>
        <tr>
            <td>Western Arizona Regional Medical Center</td>
            <td>Bullhead City</td>
            <td>AZ</td>
            <td>812.0</td>
        </tr>
        <tr>
            <td>Lovelace Medical Center</td>
            <td>Albuquerque</td>
            <td>NM</td>
            <td>813.0</td>
        </tr>
        <tr>
            <td>Peconic Bay Medical Center</td>
            <td>Riverhead</td>
            <td>NY</td>
            <td>814.0</td>
        </tr>
        <tr>
            <td>Fort Hamilton Hughes Memorial Hospital</td>
            <td>Hamilton</td>
            <td>OH</td>
            <td>815.0</td>
        </tr>
        <tr>
            <td>St. Francis Hospital</td>
            <td>Columbus</td>
            <td>GA</td>
            <td>816.0</td>
        </tr>
        <tr>
            <td>Saint Joseph&#x27;s Hospital of Atlanta</td>
            <td>Atlanta</td>
            <td>GA</td>
            <td>817.0</td>
        </tr>
        <tr>
            <td>Lake Health</td>
            <td>Concord</td>
            <td>OH</td>
            <td>818.0</td>
        </tr>
        <tr>
            <td>New York-Presbyterian Hospital</td>
            <td>New York</td>
            <td>NY</td>
            <td>819.0</td>
        </tr>
        <tr>
            <td>Mercy Health - St. Elizabeth Youngstown Hospital</td>
            <td>Youngstown</td>
            <td>OH</td>
            <td>820.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Hospital at the Vintage</td>
            <td>Houston</td>
            <td>TX</td>
            <td>821.0</td>
        </tr>
        <tr>
            <td>Atrium Health Pineville</td>
            <td>Charlotte</td>
            <td>NC</td>
            <td>822.0</td>
        </tr>
        <tr>
            <td>St. Francis-Downtown</td>
            <td>Greenville</td>
            <td>SC</td>
            <td>823.0</td>
        </tr>
        <tr>
            <td>Lakeland Hospital, St. Joseph</td>
            <td>St. Joseph</td>
            <td>MI</td>
            <td>824.0</td>
        </tr>
        <tr>
            <td>Long Beach Memorial Medical Center</td>
            <td>Long Beach</td>
            <td>CA</td>
            <td>825.0</td>
        </tr>
        <tr>
            <td>Hackensack University Medical Center</td>
            <td>Hackensack</td>
            <td>NJ</td>
            <td>826.0</td>
        </tr>
        <tr>
            <td>Texas Health HEB</td>
            <td>Bedford</td>
            <td>TX</td>
            <td>827.0</td>
        </tr>
        <tr>
            <td>St. Josephs Hospital</td>
            <td>Tampa</td>
            <td>FL</td>
            <td>828.0</td>
        </tr>
        <tr>
            <td>AdventHealth Tampa</td>
            <td>Tampa</td>
            <td>FL</td>
            <td>829.0</td>
        </tr>
        <tr>
            <td>Davis Regional Medical Center</td>
            <td>Statesville</td>
            <td>NC</td>
            <td>830.0</td>
        </tr>
        <tr>
            <td>Memorial Hermann Sugar Land Hospital</td>
            <td>Sugar Land</td>
            <td>TX</td>
            <td>831.0</td>
        </tr>
        <tr>
            <td>Ronald Reagan UCLA Medical Center</td>
            <td>Los Angeles</td>
            <td>CA</td>
            <td>832.0</td>
        </tr>
        <tr>
            <td>NYU Langone Hospitals</td>
            <td>New York</td>
            <td>NY</td>
            <td>833.0</td>
        </tr>
        <tr>
            <td>Beaumont Hospital, Grosse Pointe</td>
            <td>Grosse Pointe</td>
            <td>MI</td>
            <td>834.0</td>
        </tr>
        <tr>
            <td>HCA Houston Healthcare Kingwood</td>
            <td>Kingwood</td>
            <td>TX</td>
            <td>835.0</td>
        </tr>
        <tr>
            <td>Flaget Memorial Hospital</td>
            <td>Bardstown</td>
            <td>KY</td>
            <td>836.0</td>
        </tr>
        <tr>
            <td>Suburban Hospital</td>
            <td>Bethesda</td>
            <td>MD</td>
            <td>837.0</td>
        </tr>
        <tr>
            <td>Cleveland Clinic Avon Hospital</td>
            <td>Avon</td>
            <td>OH</td>
            <td>838.0</td>
        </tr>
        <tr>
            <td>Tennova Healthcare-Cleveland</td>
            <td>Cleveland</td>
            <td>TN</td>
            <td>839.0</td>
        </tr>
        <tr>
            <td>Memorial Medical Center Livingston</td>
            <td>Livingston</td>
            <td>TX</td>
            <td>840.0</td>
        </tr>
        <tr>
            <td>Plainview Hospital</td>
            <td>Plainview</td>
            <td>NY</td>
            <td>841.0</td>
        </tr>
        <tr>
            <td>Mount Sinai West</td>
            <td>New York</td>
            <td>NY</td>
            <td>842.0</td>
        </tr>
        <tr>
            <td>Greater Baltimore Medical Center</td>
            <td>Baltimore</td>
            <td>MD</td>
            <td>843.0</td>
        </tr>
        <tr>
            <td>Sierra Medical Center</td>
            <td>El Paso</td>
            <td>TX</td>
            <td>844.0</td>
        </tr>
        <tr>
            <td>West Boca Medical Center</td>
            <td>Boca Raton</td>
            <td>FL</td>
            <td>845.0</td>
        </tr>
        <tr>
            <td>Corona Regional Medical Center</td>
            <td>Corona</td>
            <td>CA</td>
            <td>846.0</td>
        </tr>
        <tr>
            <td>Mount Sinai Medical Center</td>
            <td>Miami Beach</td>
            <td>FL</td>
            <td>847.0</td>
        </tr>
        <tr>
            <td>Franciscan Health Crown Point</td>
            <td>Crown Point</td>
            <td>IN</td>
            <td>848.0</td>
        </tr>
        <tr>
            <td>Providence Saint John&#x27;s Health Center</td>
            <td>Santa Monica</td>
            <td>CA</td>
            <td>849.0</td>
        </tr>
        <tr>
            <td>Santa Monica - UCLA Medical Center &amp; Orthopaedic Hospital</td>
            <td>Santa Monica</td>
            <td>CA</td>
            <td>850.0</td>
        </tr>
        <tr>
            <td>South Nassau Communities Hospital</td>
            <td>Oceanside</td>
            <td>NY</td>
            <td>851.0</td>
        </tr>
        <tr>
            <td>Metropolitan Hospital Center</td>
            <td>New York</td>
            <td>NY</td>
            <td>852.0</td>
        </tr>
        <tr>
            <td>Pioneers Medical Center</td>
            <td>Meeker</td>
            <td>CO</td>
            <td>853.0</td>
        </tr>
        <tr>
            <td>St. Charles Madras</td>
            <td>Madras</td>
            <td>OR</td>
            <td>854.0</td>
        </tr>
        <tr>
            <td>Heber Valley Hospital</td>
            <td>Heber City</td>
            <td>UT</td>
            <td>855.0</td>
        </tr>
        <tr>
            <td>North Vista Hospital</td>
            <td>North Las Vegas</td>
            <td>NV</td>
            <td>856.0</td>
        </tr>
        <tr>
            <td>Whitman Hospital and Medical Center</td>
            <td>Colfax</td>
            <td>WA</td>
            <td>857.0</td>
        </tr>
        <tr>
            <td>Tufts Medical Center</td>
            <td>Boston</td>
            <td>MA</td>
            <td>858.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System-Northland</td>
            <td>Barron</td>
            <td>WI</td>
            <td>859.0</td>
        </tr>
        <tr>
            <td>Colleton Medical Center</td>
            <td>Walterboro</td>
            <td>SC</td>
            <td>860.0</td>
        </tr>
        <tr>
            <td>Central Montana Medical Center</td>
            <td>Lewistown</td>
            <td>MT</td>
            <td>861.0</td>
        </tr>
        <tr>
            <td>Adventist Health Ukiah Valley</td>
            <td>Ukiah</td>
            <td>CA</td>
            <td>862.0</td>
        </tr>
        <tr>
            <td>Bronson Lakeview Hospital</td>
            <td>Paw Paw</td>
            <td>MI</td>
            <td>863.0</td>
        </tr>
        <tr>
            <td>Chatham Hospital</td>
            <td>Siler City</td>
            <td>NC</td>
            <td>864.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Nampa Medical Center</td>
            <td>Nampa</td>
            <td>ID</td>
            <td>865.0</td>
        </tr>
        <tr>
            <td>Parkland Health and Hospital System</td>
            <td>Dallas</td>
            <td>TX</td>
            <td>866.0</td>
        </tr>
        <tr>
            <td>Milan General Hospital</td>
            <td>Milan</td>
            <td>TN</td>
            <td>867.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System - Red Cedar</td>
            <td>Menomonie</td>
            <td>WI</td>
            <td>868.0</td>
        </tr>
        <tr>
            <td>Southwest General Hospital</td>
            <td>San Antonio</td>
            <td>TX</td>
            <td>869.0</td>
        </tr>
        <tr>
            <td>CHI Mercy Health</td>
            <td>Valley City</td>
            <td>ND</td>
            <td>870.0</td>
        </tr>
        <tr>
            <td>White Memorial Medical Center</td>
            <td>Los Angeles</td>
            <td>CA</td>
            <td>871.0</td>
        </tr>
        <tr>
            <td>Providence St. Joseph Hospital</td>
            <td>Chewelah</td>
            <td>WA</td>
            <td>872.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital and Medical Center</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>873.0</td>
        </tr>
        <tr>
            <td>Regions Hospital</td>
            <td>Saint Paul</td>
            <td>MN</td>
            <td>874.0</td>
        </tr>
        <tr>
            <td>Indiana University Health Frankfort</td>
            <td>Frankfort</td>
            <td>IN</td>
            <td>875.0</td>
        </tr>
        <tr>
            <td>Bergen New Bridge Medical Center</td>
            <td>Paramus</td>
            <td>NJ</td>
            <td>876.0</td>
        </tr>
        <tr>
            <td>Southside Community Hospital</td>
            <td>Farmville</td>
            <td>VA</td>
            <td>877.0</td>
        </tr>
        <tr>
            <td>The University of Chicago Medical Center</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>878.0</td>
        </tr>
        <tr>
            <td>University of Missouri Health Care</td>
            <td>Columbia</td>
            <td>MO</td>
            <td>879.0</td>
        </tr>
        <tr>
            <td>Bridgton Hospital</td>
            <td>Bridgton</td>
            <td>ME</td>
            <td>880.0</td>
        </tr>
        <tr>
            <td>Providence Seaside Hospital</td>
            <td>Seaside</td>
            <td>OR</td>
            <td>881.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System-New Prague</td>
            <td>New Prague</td>
            <td>MN</td>
            <td>882.0</td>
        </tr>
        <tr>
            <td>Spectrum Health Gerber Memorial</td>
            <td>Fremont</td>
            <td>MI</td>
            <td>883.0</td>
        </tr>
        <tr>
            <td>Sherman Oaks Hospital</td>
            <td>Sherman Oaks</td>
            <td>CA</td>
            <td>884.0</td>
        </tr>
        <tr>
            <td>Elliot Hospital</td>
            <td>Manchester</td>
            <td>NH</td>
            <td>885.0</td>
        </tr>
        <tr>
            <td>UPMC Horizon</td>
            <td>Greenville</td>
            <td>PA</td>
            <td>886.0</td>
        </tr>
        <tr>
            <td>Wellstar Atlanta Medical Center</td>
            <td>Atlanta</td>
            <td>GA</td>
            <td>887.0</td>
        </tr>
        <tr>
            <td>Ohio State University Hospitals</td>
            <td>Columbus</td>
            <td>OH</td>
            <td>889.0</td>
        </tr>
        <tr>
            <td>Miami County Medical Center</td>
            <td>Paola</td>
            <td>KS</td>
            <td>890.0</td>
        </tr>
        <tr>
            <td>West Virginia University Hospitals</td>
            <td>Morgantown</td>
            <td>WV</td>
            <td>891.0</td>
        </tr>
        <tr>
            <td>Palms West Hospital</td>
            <td>Loxahatchee</td>
            <td>FL</td>
            <td>892.0</td>
        </tr>
        <tr>
            <td>Rochester General Hospital</td>
            <td>Rochester</td>
            <td>NY</td>
            <td>893.0</td>
        </tr>
        <tr>
            <td>Sacred Heart Medical Center - Riverbend</td>
            <td>Springfield</td>
            <td>OR</td>
            <td>894.0</td>
        </tr>
        <tr>
            <td>PeaceHealth Southwest Medical Center</td>
            <td>Vancouver</td>
            <td>WA</td>
            <td>895.0</td>
        </tr>
        <tr>
            <td>Community Hospital</td>
            <td>Tallassee</td>
            <td>AL</td>
            <td>896.0</td>
        </tr>
        <tr>
            <td>Bon Secours Memorial Regional Medical Center</td>
            <td>Mechanicsville</td>
            <td>VA</td>
            <td>897.0</td>
        </tr>
        <tr>
            <td>Newark-Wayne Community Hospital</td>
            <td>Newark</td>
            <td>NY</td>
            <td>899.0</td>
        </tr>
        <tr>
            <td>University of Maryland Medical Center</td>
            <td>Baltimore</td>
            <td>MD</td>
            <td>900.0</td>
        </tr>
        <tr>
            <td>Carolinas Healthcare System Stanly</td>
            <td>Albemarle</td>
            <td>NC</td>
            <td>901.0</td>
        </tr>
        <tr>
            <td>Amery Hospital &amp; Clinic</td>
            <td>Amery</td>
            <td>WI</td>
            <td>902.0</td>
        </tr>
        <tr>
            <td>Good Shepherd Medical Center</td>
            <td>Hermiston</td>
            <td>OR</td>
            <td>903.0</td>
        </tr>
        <tr>
            <td>Dominican Hospital</td>
            <td>Santa Cruz</td>
            <td>CA</td>
            <td>904.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Quakertown Hospital</td>
            <td>Quakertown</td>
            <td>PA</td>
            <td>905.0</td>
        </tr>
        <tr>
            <td>UNM Sandoval Regional Medical Center</td>
            <td>Rio Rancho</td>
            <td>NM</td>
            <td>906.0</td>
        </tr>
        <tr>
            <td>Fairview Hospital</td>
            <td>Great Barrington</td>
            <td>MA</td>
            <td>907.0</td>
        </tr>
        <tr>
            <td>Nathan Littauer Hospital</td>
            <td>Gloversville</td>
            <td>NY</td>
            <td>908.0</td>
        </tr>
        <tr>
            <td>The Carle Foundation Hospital</td>
            <td>Urbana</td>
            <td>IL</td>
            <td>909.0</td>
        </tr>
        <tr>
            <td>University of Cincinnati Medical Center</td>
            <td>Cincinnati</td>
            <td>OH</td>
            <td>910.0</td>
        </tr>
        <tr>
            <td>Saint Francis Hospital Muskogee</td>
            <td>Muskogee</td>
            <td>OK</td>
            <td>911.0</td>
        </tr>
        <tr>
            <td>HCA Houston Healthcare Northwest</td>
            <td>Houston</td>
            <td>TX</td>
            <td>912.0</td>
        </tr>
        <tr>
            <td>Essentia Health Virginia</td>
            <td>Virginia</td>
            <td>MN</td>
            <td>913.0</td>
        </tr>
        <tr>
            <td>UMass Memorial Medical Center</td>
            <td>Worcester</td>
            <td>MA</td>
            <td>914.0</td>
        </tr>
        <tr>
            <td>Carilion Stonewall Jackson Hospital</td>
            <td>Lexington</td>
            <td>VA</td>
            <td>915.0</td>
        </tr>
        <tr>
            <td>Montclair Hospital Medical Center</td>
            <td>Montclair</td>
            <td>CA</td>
            <td>916.0</td>
        </tr>
        <tr>
            <td>Sanford Bemidji Medical Center</td>
            <td>Bemidji</td>
            <td>MN</td>
            <td>917.0</td>
        </tr>
        <tr>
            <td>Carolinas Healthcare System Union</td>
            <td>Monroe</td>
            <td>NC</td>
            <td>918.0</td>
        </tr>
        <tr>
            <td>Platte Valley Medical Center</td>
            <td>Brighton</td>
            <td>CO</td>
            <td>919.0</td>
        </tr>
        <tr>
            <td>The Hospital of Central Connecticut</td>
            <td>New Britain</td>
            <td>CT</td>
            <td>920.0</td>
        </tr>
        <tr>
            <td>UPMC Mckeesport</td>
            <td>McKeesport</td>
            <td>PA</td>
            <td>921.0</td>
        </tr>
        <tr>
            <td>Bon Secours-St. Francis Xavier Hospital</td>
            <td>Charleston</td>
            <td>SC</td>
            <td>922.0</td>
        </tr>
        <tr>
            <td>Baptist Health Medical Center- Conway</td>
            <td>Conway</td>
            <td>AR</td>
            <td>923.0</td>
        </tr>
        <tr>
            <td>Alvarado Hospital Medical Center</td>
            <td>San Diego</td>
            <td>CA</td>
            <td>924.0</td>
        </tr>
        <tr>
            <td>West Anaheim Medical Center</td>
            <td>Anaheim</td>
            <td>CA</td>
            <td>925.0</td>
        </tr>
        <tr>
            <td>George Washington University Hospital</td>
            <td>Washington</td>
            <td>DC</td>
            <td>926.0</td>
        </tr>
        <tr>
            <td>MUSC Medical Center</td>
            <td>Charleston</td>
            <td>SC</td>
            <td>927.0</td>
        </tr>
        <tr>
            <td>Legacy Emanuel Medical Center</td>
            <td>Portland</td>
            <td>OR</td>
            <td>928.0</td>
        </tr>
        <tr>
            <td>Porter Hospital</td>
            <td>Middlebury</td>
            <td>VT</td>
            <td>929.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Tishomingo</td>
            <td>Tishomingo</td>
            <td>OK</td>
            <td>930.0</td>
        </tr>
        <tr>
            <td>Parkview Medical Center</td>
            <td>Pueblo</td>
            <td>CO</td>
            <td>931.0</td>
        </tr>
        <tr>
            <td>Hunterdon Medical Center</td>
            <td>Flemington</td>
            <td>NJ</td>
            <td>932.0</td>
        </tr>
        <tr>
            <td>Franklin Memorial Hospital</td>
            <td>Farmington</td>
            <td>ME</td>
            <td>933.0</td>
        </tr>
        <tr>
            <td>Tuality Community Hospital</td>
            <td>Hillsboro</td>
            <td>OR</td>
            <td>934.0</td>
        </tr>
        <tr>
            <td>Bitterroot Health</td>
            <td>Hamilton</td>
            <td>MT</td>
            <td>935.0</td>
        </tr>
        <tr>
            <td>Banner Estrella Medical Center</td>
            <td>Phoenix</td>
            <td>AZ</td>
            <td>936.0</td>
        </tr>
        <tr>
            <td>OhioHealth Grant Medical Center</td>
            <td>Columbus</td>
            <td>OH</td>
            <td>937.0</td>
        </tr>
        <tr>
            <td>Sentara Albemarle Medical Center</td>
            <td>Elizabeth City</td>
            <td>NC</td>
            <td>938.0</td>
        </tr>
        <tr>
            <td>AdventHealth Murray</td>
            <td>Chatsworth</td>
            <td>GA</td>
            <td>940.0</td>
        </tr>
        <tr>
            <td>Bell Hospital</td>
            <td>Ishpeming</td>
            <td>MI</td>
            <td>941.0</td>
        </tr>
        <tr>
            <td>Geisinger Medical Center</td>
            <td>Danville</td>
            <td>PA</td>
            <td>942.0</td>
        </tr>
        <tr>
            <td>Spectrum Health United Hospital</td>
            <td>Greenville</td>
            <td>MI</td>
            <td>943.0</td>
        </tr>
        <tr>
            <td>Adventist Health Bakersfield</td>
            <td>Bakersfield</td>
            <td>CA</td>
            <td>944.0</td>
        </tr>
        <tr>
            <td>War Memorial Hospital</td>
            <td>Berkeley Springs</td>
            <td>WV</td>
            <td>945.0</td>
        </tr>
        <tr>
            <td>Sunrise Hospital and Medical Center</td>
            <td>Las Vegas</td>
            <td>NV</td>
            <td>946.0</td>
        </tr>
        <tr>
            <td>Deer River Healthcare Center</td>
            <td>Deer River</td>
            <td>MN</td>
            <td>947.0</td>
        </tr>
        <tr>
            <td>Tahoe Forest Hospital</td>
            <td>Truckee</td>
            <td>CA</td>
            <td>948.0</td>
        </tr>
        <tr>
            <td>Sentara Halifax Regional Hospital</td>
            <td>South Boston</td>
            <td>VA</td>
            <td>949.0</td>
        </tr>
        <tr>
            <td>Mount St. Mary&#x27;s Hospital AndÂ¬â€  Health Center</td>
            <td>Lewiston</td>
            <td>NY</td>
            <td>950.0</td>
        </tr>
        <tr>
            <td>Ascension Our Lady of Victory Hospital</td>
            <td>Stanley</td>
            <td>WI</td>
            <td>951.0</td>
        </tr>
        <tr>
            <td>University of Toledo Medical Center</td>
            <td>Toledo</td>
            <td>OH</td>
            <td>952.0</td>
        </tr>
        <tr>
            <td>Sanford Mayville</td>
            <td>Mayville</td>
            <td>ND</td>
            <td>953.0</td>
        </tr>
        <tr>
            <td>Mercy Harvard Hospital</td>
            <td>Harvard</td>
            <td>IL</td>
            <td>954.0</td>
        </tr>
        <tr>
            <td>Centracare Health - Monticello</td>
            <td>Monticello</td>
            <td>MN</td>
            <td>955.0</td>
        </tr>
        <tr>
            <td>Integris Southwest Medical Center</td>
            <td>Oklahoma City</td>
            <td>OK</td>
            <td>956.0</td>
        </tr>
        <tr>
            <td>Erlanger Medical Center</td>
            <td>Chattanooga</td>
            <td>TN</td>
            <td>957.0</td>
        </tr>
        <tr>
            <td>Lincoln Health</td>
            <td>Damariscotta</td>
            <td>ME</td>
            <td>958.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital Jacksonville</td>
            <td>Jacksonville</td>
            <td>FL</td>
            <td>959.0</td>
        </tr>
        <tr>
            <td>Palmdale Regional Medical Center</td>
            <td>Palmdale</td>
            <td>CA</td>
            <td>960.0</td>
        </tr>
        <tr>
            <td>St. Mary&#x27;s Hospital</td>
            <td>Athens</td>
            <td>GA</td>
            <td>961.0</td>
        </tr>
        <tr>
            <td>Loma Linda University Medical Center</td>
            <td>Loma Linda</td>
            <td>CA</td>
            <td>962.0</td>
        </tr>
        <tr>
            <td>University of Maryland Shore Medical Center at Chestertown</td>
            <td>Chestertown</td>
            <td>MD</td>
            <td>963.0</td>
        </tr>
        <tr>
            <td>Medstar Union Memorial Hospital</td>
            <td>Baltimore</td>
            <td>MD</td>
            <td>964.0</td>
        </tr>
        <tr>
            <td>Greater El Monte Community Hospital</td>
            <td>South El Monte</td>
            <td>CA</td>
            <td>965.0</td>
        </tr>
        <tr>
            <td>Lawnwood Regional Medical Center &amp; Heart Institute</td>
            <td>Fort Pierce</td>
            <td>FL</td>
            <td>966.0</td>
        </tr>
        <tr>
            <td>Banner Payson Medical Center</td>
            <td>Payson</td>
            <td>AZ</td>
            <td>967.0</td>
        </tr>
        <tr>
            <td>Our Lady of Lourdes Memorial Hospital</td>
            <td>Binghamton</td>
            <td>NY</td>
            <td>968.0</td>
        </tr>
        <tr>
            <td>Sacred Heart Hospital on the Gulf</td>
            <td>Port Saint Joe</td>
            <td>FL</td>
            <td>969.0</td>
        </tr>
        <tr>
            <td>Good Samaritan Regional Medical Center</td>
            <td>Corvallis</td>
            <td>OR</td>
            <td>970.0</td>
        </tr>
        <tr>
            <td>The Johns Hopkins Hospital</td>
            <td>Baltimore</td>
            <td>MD</td>
            <td>971.0</td>
        </tr>
        <tr>
            <td>Chippewa County War Memorial Hospital</td>
            <td>Sault Sainte Marie</td>
            <td>MI</td>
            <td>972.0</td>
        </tr>
        <tr>
            <td>Baptist Health Richmond</td>
            <td>Richmond</td>
            <td>KY</td>
            <td>973.0</td>
        </tr>
        <tr>
            <td>Weirton Medical Center</td>
            <td>Weirton</td>
            <td>WV</td>
            <td>974.0</td>
        </tr>
        <tr>
            <td>Essentia Health St. Mary&#x27;s Hospital - Superior</td>
            <td>Superior</td>
            <td>WI</td>
            <td>975.0</td>
        </tr>
        <tr>
            <td>Belton Regional Medical Center</td>
            <td>Belton</td>
            <td>MO</td>
            <td>976.0</td>
        </tr>
        <tr>
            <td>Ascension All Saints Hospital</td>
            <td>Racine</td>
            <td>WI</td>
            <td>978.0</td>
        </tr>
        <tr>
            <td>Adventist Health and Rideout</td>
            <td>Marysville</td>
            <td>CA</td>
            <td>979.0</td>
        </tr>
        <tr>
            <td>Mercy Medical Center Redding</td>
            <td>Redding</td>
            <td>CA</td>
            <td>980.0</td>
        </tr>
        <tr>
            <td>Cabell Huntington Hospital</td>
            <td>Huntington</td>
            <td>WV</td>
            <td>981.0</td>
        </tr>
        <tr>
            <td>St. Elizabeth Medical Center North</td>
            <td>Edgewood</td>
            <td>KY</td>
            <td>982.0</td>
        </tr>
        <tr>
            <td>Conway Regional Health System</td>
            <td>Conway</td>
            <td>AR</td>
            <td>983.0</td>
        </tr>
        <tr>
            <td>Willamette Valley Medical Center</td>
            <td>McMinnville</td>
            <td>OR</td>
            <td>984.0</td>
        </tr>
        <tr>
            <td>Freeman Neosho Hospital</td>
            <td>Neosho</td>
            <td>MO</td>
            <td>985.0</td>
        </tr>
        <tr>
            <td>Concord Hospital</td>
            <td>Concord</td>
            <td>NH</td>
            <td>986.0</td>
        </tr>
        <tr>
            <td>Mississippi Baptist Medical Center</td>
            <td>Jackson</td>
            <td>MS</td>
            <td>987.0</td>
        </tr>
        <tr>
            <td>Tri County Hospital</td>
            <td>Wadena</td>
            <td>MN</td>
            <td>988.0</td>
        </tr>
        <tr>
            <td>Newark Beth Israel Medical Center</td>
            <td>Newark</td>
            <td>NJ</td>
            <td>989.0</td>
        </tr>
        <tr>
            <td>Providence Regional Medical Center Everett</td>
            <td>Everett</td>
            <td>WA</td>
            <td>990.0</td>
        </tr>
        <tr>
            <td>Murphy Medical Center</td>
            <td>Murphy</td>
            <td>NC</td>
            <td>991.0</td>
        </tr>
        <tr>
            <td>Community Hospital East</td>
            <td>Indianapolis</td>
            <td>IN</td>
            <td>993.0</td>
        </tr>
        <tr>
            <td>Methodist Hospital South</td>
            <td>Jourdanton</td>
            <td>TX</td>
            <td>994.0</td>
        </tr>
        <tr>
            <td>Grady General Hospital</td>
            <td>Cairo</td>
            <td>GA</td>
            <td>995.0</td>
        </tr>
        <tr>
            <td>Hill Country Memorial Hospital</td>
            <td>Fredericksburg</td>
            <td>TX</td>
            <td>996.0</td>
        </tr>
        <tr>
            <td>Coshocton Regional Medical Center</td>
            <td>Coshocton</td>
            <td>OH</td>
            <td>997.0</td>
        </tr>
        <tr>
            <td>Conway Medical Center</td>
            <td>Conway</td>
            <td>SC</td>
            <td>998.0</td>
        </tr>
        <tr>
            <td>Cortland Regional Medical Center</td>
            <td>Cortland</td>
            <td>NY</td>
            <td>999.0</td>
        </tr>
        <tr>
            <td>CPMC Davies Campus</td>
            <td>San Francisco</td>
            <td>CA</td>
            <td>1000.0</td>
        </tr>
        <tr>
            <td>Northern Maine Medical Center</td>
            <td>Fort Kent</td>
            <td>ME</td>
            <td>1001.0</td>
        </tr>
        <tr>
            <td>West Jefferson Medical Center</td>
            <td>Marrero</td>
            <td>LA</td>
            <td>1002.0</td>
        </tr>
        <tr>
            <td>Presence Saint Joseph Hospital - Elgin</td>
            <td>Elgin</td>
            <td>IL</td>
            <td>1003.0</td>
        </tr>
        <tr>
            <td>Marlborough Hospital</td>
            <td>Marlborough</td>
            <td>MA</td>
            <td>1004.0</td>
        </tr>
        <tr>
            <td>Wray Community District Hospital</td>
            <td>Wray</td>
            <td>CO</td>
            <td>1005.0</td>
        </tr>
        <tr>
            <td>Mclaren Oakland</td>
            <td>Pontiac</td>
            <td>MI</td>
            <td>1006.0</td>
        </tr>
        <tr>
            <td>University of Maryland Prince George&#x27;s Hospital Center</td>
            <td>Cheverly</td>
            <td>MD</td>
            <td>1008.0</td>
        </tr>
        <tr>
            <td>Western Wisconsin Health</td>
            <td>Baldwin</td>
            <td>WI</td>
            <td>1009.0</td>
        </tr>
        <tr>
            <td>St. Mary&#x27;s Regional Medical Center</td>
            <td>Lewiston</td>
            <td>ME</td>
            <td>1010.0</td>
        </tr>
        <tr>
            <td>St. Lucie Medical Center</td>
            <td>Port Saint Lucie</td>
            <td>FL</td>
            <td>1011.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Cornwall Hospital</td>
            <td>Newburgh</td>
            <td>NY</td>
            <td>1012.0</td>
        </tr>
        <tr>
            <td>St. Thomas More Hospital</td>
            <td>Canon City</td>
            <td>CO</td>
            <td>1013.0</td>
        </tr>
        <tr>
            <td>Plumas District Hospital</td>
            <td>Quincy</td>
            <td>CA</td>
            <td>1014.0</td>
        </tr>
        <tr>
            <td>UPMC Mercy</td>
            <td>Pittsburgh</td>
            <td>PA</td>
            <td>1015.0</td>
        </tr>
        <tr>
            <td>Bridgeport Hospital</td>
            <td>Bridgeport</td>
            <td>CT</td>
            <td>1016.0</td>
        </tr>
        <tr>
            <td>Mercy Tiffin Hospital</td>
            <td>Tiffin</td>
            <td>OH</td>
            <td>1017.0</td>
        </tr>
        <tr>
            <td>Columbus Regional Hospital</td>
            <td>Columbus</td>
            <td>IN</td>
            <td>1018.0</td>
        </tr>
        <tr>
            <td>Gwinnett Medical Center</td>
            <td>Lawrenceville</td>
            <td>GA</td>
            <td>1019.0</td>
        </tr>
        <tr>
            <td>Avera Holy Family Hospital</td>
            <td>Estherville</td>
            <td>IA</td>
            <td>1020.0</td>
        </tr>
        <tr>
            <td>UT Health East Texas Pittsburg Hospital</td>
            <td>Pittsburg</td>
            <td>TX</td>
            <td>1021.0</td>
        </tr>
        <tr>
            <td>UCHealth Pikes Peak Regional Hospital</td>
            <td>Woodland Park</td>
            <td>CO</td>
            <td>1022.0</td>
        </tr>
        <tr>
            <td>Saint Agnes Medical Center</td>
            <td>Fresno</td>
            <td>CA</td>
            <td>1023.0</td>
        </tr>
        <tr>
            <td>Harper University Hospital</td>
            <td>Detroit</td>
            <td>MI</td>
            <td>1024.0</td>
        </tr>
        <tr>
            <td>Berkshire Medical Center Inc</td>
            <td>Pittsfield</td>
            <td>MA</td>
            <td>1025.0</td>
        </tr>
        <tr>
            <td>Johnston Memorial Hospital</td>
            <td>Abingdon</td>
            <td>VA</td>
            <td>1026.0</td>
        </tr>
        <tr>
            <td>Lovelace Women&#x27;s Hospital</td>
            <td>Albuquerque</td>
            <td>NM</td>
            <td>1027.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Springfield</td>
            <td>Springfield</td>
            <td>MO</td>
            <td>1028.0</td>
        </tr>
        <tr>
            <td>Milford Regional Medical Center</td>
            <td>Milford</td>
            <td>MA</td>
            <td>1029.0</td>
        </tr>
        <tr>
            <td>Delta Community Hospital</td>
            <td>Delta</td>
            <td>UT</td>
            <td>1030.0</td>
        </tr>
        <tr>
            <td>Jacobi Medical Center</td>
            <td>Bronx</td>
            <td>NY</td>
            <td>1031.0</td>
        </tr>
        <tr>
            <td>Indiana University Health White Memorial Hospital</td>
            <td>Monticello</td>
            <td>IN</td>
            <td>1032.0</td>
        </tr>
        <tr>
            <td>Chino Valley Medical Center</td>
            <td>Chino</td>
            <td>CA</td>
            <td>1033.0</td>
        </tr>
        <tr>
            <td>Sycamore Shoals Hospital</td>
            <td>Elizabethton</td>
            <td>TN</td>
            <td>1034.0</td>
        </tr>
        <tr>
            <td>Holy Cross Germantown Hospital</td>
            <td>Germantown</td>
            <td>MD</td>
            <td>1035.0</td>
        </tr>
        <tr>
            <td>Jamaica Hospital Medical Center</td>
            <td>Jamaica</td>
            <td>NY</td>
            <td>1036.0</td>
        </tr>
        <tr>
            <td>Trident Medical Center</td>
            <td>Charleston</td>
            <td>SC</td>
            <td>1037.0</td>
        </tr>
        <tr>
            <td>Ochsner Medical Center - Baton Rouge</td>
            <td>Baton Rouge</td>
            <td>LA</td>
            <td>1038.0</td>
        </tr>
        <tr>
            <td>AdventHealth Dade City</td>
            <td>Dade City</td>
            <td>FL</td>
            <td>1039.0</td>
        </tr>
        <tr>
            <td>Meritus Medical Center</td>
            <td>Hagerstown</td>
            <td>MD</td>
            <td>1041.0</td>
        </tr>
        <tr>
            <td>Medical City North Hills</td>
            <td>North Richland Hills</td>
            <td>TX</td>
            <td>1042.0</td>
        </tr>
        <tr>
            <td>Pella Regional Health Center</td>
            <td>Pella</td>
            <td>IA</td>
            <td>1043.0</td>
        </tr>
        <tr>
            <td>King&#x27;s Daughters&#x27; Medical Center</td>
            <td>Ashland</td>
            <td>KY</td>
            <td>1044.0</td>
        </tr>
        <tr>
            <td>Baylor Scott and White Medical Center Carrollton</td>
            <td>Carrollton</td>
            <td>TX</td>
            <td>1045.0</td>
        </tr>
        <tr>
            <td>Renown Regional Medical Center</td>
            <td>Reno</td>
            <td>NV</td>
            <td>1046.0</td>
        </tr>
        <tr>
            <td>Wright Memorial Hospital</td>
            <td>Trenton</td>
            <td>MO</td>
            <td>1047.0</td>
        </tr>
        <tr>
            <td>Strong Memorial Hospital</td>
            <td>Rochester</td>
            <td>NY</td>
            <td>1048.0</td>
        </tr>
        <tr>
            <td>Jackson Healthcare Center</td>
            <td>Edna</td>
            <td>TX</td>
            <td>1049.0</td>
        </tr>
        <tr>
            <td>Hereford Regional Medical Center</td>
            <td>Hereford</td>
            <td>TX</td>
            <td>1050.0</td>
        </tr>
        <tr>
            <td>Geisinger-Lewistown Hospital</td>
            <td>Lewistown</td>
            <td>PA</td>
            <td>1051.0</td>
        </tr>
        <tr>
            <td>Seton Smithville Regional Hospital</td>
            <td>Smithville</td>
            <td>TX</td>
            <td>1052.0</td>
        </tr>
        <tr>
            <td>Glendale Adventist Medical Center</td>
            <td>Glendale</td>
            <td>CA</td>
            <td>1053.0</td>
        </tr>
        <tr>
            <td>Sacred Heart University District</td>
            <td>Eugene</td>
            <td>OR</td>
            <td>1054.0</td>
        </tr>
        <tr>
            <td>Emory Hillandale Hospital</td>
            <td>Lithonia</td>
            <td>GA</td>
            <td>1055.0</td>
        </tr>
        <tr>
            <td>UPMC Cole</td>
            <td>Coudersport</td>
            <td>PA</td>
            <td>1056.0</td>
        </tr>
        <tr>
            <td>LA Downtown Medical Center</td>
            <td>Los Angeles</td>
            <td>CA</td>
            <td>1057.0</td>
        </tr>
        <tr>
            <td>South Texas Health System</td>
            <td>Edinburg</td>
            <td>TX</td>
            <td>1058.0</td>
        </tr>
        <tr>
            <td>Phelps Memorial Health Center</td>
            <td>Holdrege</td>
            <td>NE</td>
            <td>1059.0</td>
        </tr>
        <tr>
            <td>Saint Joseph London</td>
            <td>London</td>
            <td>KY</td>
            <td>1060.0</td>
        </tr>
        <tr>
            <td>Bartlett Regional Hospital</td>
            <td>Juneau</td>
            <td>AK</td>
            <td>1061.0</td>
        </tr>
        <tr>
            <td>Lakes Region General Hospital</td>
            <td>Laconia</td>
            <td>NH</td>
            <td>1062.0</td>
        </tr>
        <tr>
            <td>Ogallala Community Hospital</td>
            <td>Ogallala</td>
            <td>NE</td>
            <td>1063.0</td>
        </tr>
        <tr>
            <td>Saint Agnes Hospital</td>
            <td>Baltimore</td>
            <td>MD</td>
            <td>1064.0</td>
        </tr>
        <tr>
            <td>Aspirus Keweenaw Hospital</td>
            <td>Laurium</td>
            <td>MI</td>
            <td>1065.0</td>
        </tr>
        <tr>
            <td>University of Maryland Shore Medical Center at Easton</td>
            <td>Easton</td>
            <td>MD</td>
            <td>1066.0</td>
        </tr>
        <tr>
            <td>Memorial Health University Medical Center</td>
            <td>Savannah</td>
            <td>GA</td>
            <td>1067.0</td>
        </tr>
        <tr>
            <td>Bellevue Hospital</td>
            <td>Bellevue</td>
            <td>OH</td>
            <td>1068.0</td>
        </tr>
        <tr>
            <td>Gundersen St. Josephs Hospital and Clinics</td>
            <td>Hillsboro</td>
            <td>WI</td>
            <td>1069.0</td>
        </tr>
        <tr>
            <td>Trios</td>
            <td>Kennewick</td>
            <td>WA</td>
            <td>1070.0</td>
        </tr>
        <tr>
            <td>Bronson South Haven Hospital</td>
            <td>South Haven</td>
            <td>MI</td>
            <td>1071.0</td>
        </tr>
        <tr>
            <td>Ascension Via Christi Hospitals Wichita</td>
            <td>Wichita</td>
            <td>KS</td>
            <td>1072.0</td>
        </tr>
        <tr>
            <td>Holston Valley Medical Center</td>
            <td>Kingsport</td>
            <td>TN</td>
            <td>1073.0</td>
        </tr>
        <tr>
            <td>Shasta Regional Medical Center</td>
            <td>Redding</td>
            <td>CA</td>
            <td>1074.0</td>
        </tr>
        <tr>
            <td>Decatur Morgan Hospital-Decatur Campus</td>
            <td>Decatur</td>
            <td>AL</td>
            <td>1075.0</td>
        </tr>
        <tr>
            <td>Riverside Community Hospital</td>
            <td>Riverside</td>
            <td>CA</td>
            <td>1076.0</td>
        </tr>
        <tr>
            <td>Health Central</td>
            <td>Ocoee</td>
            <td>FL</td>
            <td>1077.0</td>
        </tr>
        <tr>
            <td>Adventhealth Wauchula</td>
            <td>Wauchula</td>
            <td>FL</td>
            <td>1078.0</td>
        </tr>
        <tr>
            <td>White County Medical Center</td>
            <td>Searcy</td>
            <td>AR</td>
            <td>1079.0</td>
        </tr>
        <tr>
            <td>Skiff Medical Center</td>
            <td>Newton</td>
            <td>IA</td>
            <td>1080.0</td>
        </tr>
        <tr>
            <td>Adirondack Medical Center - Physician</td>
            <td>Saranac Lake</td>
            <td>NY</td>
            <td>1081.0</td>
        </tr>
        <tr>
            <td>Edgerton Hospital And Health Services</td>
            <td>Edgerton</td>
            <td>WI</td>
            <td>1082.0</td>
        </tr>
        <tr>
            <td>AdventHealth Fish Memorial</td>
            <td>Orange City</td>
            <td>FL</td>
            <td>1083.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Lincoln</td>
            <td>Troy</td>
            <td>MO</td>
            <td>1084.0</td>
        </tr>
        <tr>
            <td>Reedsburg Area Medical Center</td>
            <td>Reedsburg</td>
            <td>WI</td>
            <td>1085.0</td>
        </tr>
        <tr>
            <td>Raritan Bay Medical Center Perth Amboy Division</td>
            <td>Perth Amboy</td>
            <td>NJ</td>
            <td>1086.0</td>
        </tr>
        <tr>
            <td>Tidelands Health</td>
            <td>Georgetown</td>
            <td>SC</td>
            <td>1087.0</td>
        </tr>
        <tr>
            <td>Unity Hospital of Rochester</td>
            <td>Rochester</td>
            <td>NY</td>
            <td>1088.0</td>
        </tr>
        <tr>
            <td>Elkview General Hospital</td>
            <td>Hobart</td>
            <td>OK</td>
            <td>1089.0</td>
        </tr>
        <tr>
            <td>Methodist Hospital of Sacramento</td>
            <td>Sacramento</td>
            <td>CA</td>
            <td>1090.0</td>
        </tr>
        <tr>
            <td>Bristol Hospital</td>
            <td>Bristol</td>
            <td>CT</td>
            <td>1091.0</td>
        </tr>
        <tr>
            <td>St. Luke Community Hospital</td>
            <td>Ronan</td>
            <td>MT</td>
            <td>1092.0</td>
        </tr>
        <tr>
            <td>Scotland County  Hospital</td>
            <td>Memphis</td>
            <td>MO</td>
            <td>1093.0</td>
        </tr>
        <tr>
            <td>University Hospital SUNY Health Science Center</td>
            <td>Syracuse</td>
            <td>NY</td>
            <td>1094.0</td>
        </tr>
        <tr>
            <td>Lompoc Valley Medical Center</td>
            <td>Lompoc</td>
            <td>CA</td>
            <td>1095.0</td>
        </tr>
        <tr>
            <td>Carrington Health Center</td>
            <td>Carrington</td>
            <td>ND</td>
            <td>1096.0</td>
        </tr>
        <tr>
            <td>Coon Memorial Hospital</td>
            <td>Dalhart</td>
            <td>TX</td>
            <td>1097.0</td>
        </tr>
        <tr>
            <td>Mount Sinai Beth Israel</td>
            <td>New York</td>
            <td>NY</td>
            <td>1098.0</td>
        </tr>
        <tr>
            <td>Putnam Community Medical Center</td>
            <td>Palatka</td>
            <td>FL</td>
            <td>1099.0</td>
        </tr>
        <tr>
            <td>Mccullough-Hyde Memorial Hospital</td>
            <td>Oxford</td>
            <td>OH</td>
            <td>1100.0</td>
        </tr>
        <tr>
            <td>Teche Regional Medical Center</td>
            <td>Morgan City</td>
            <td>LA</td>
            <td>1101.0</td>
        </tr>
        <tr>
            <td>Southside Hospital</td>
            <td>Bay Shore</td>
            <td>NY</td>
            <td>1102.0</td>
        </tr>
        <tr>
            <td>Alameda Hospital</td>
            <td>Alameda</td>
            <td>CA</td>
            <td>1103.0</td>
        </tr>
        <tr>
            <td>Garden City Hospital</td>
            <td>Garden City</td>
            <td>MI</td>
            <td>1104.0</td>
        </tr>
        <tr>
            <td>Valley Hospital Medical Center</td>
            <td>Las Vegas</td>
            <td>NV</td>
            <td>1105.0</td>
        </tr>
        <tr>
            <td>Beaumont Hospital - Farmington Hills</td>
            <td>Farmington Hills</td>
            <td>MI</td>
            <td>1106.0</td>
        </tr>
        <tr>
            <td>Higgins General Hospital</td>
            <td>Bremen</td>
            <td>GA</td>
            <td>1107.0</td>
        </tr>
        <tr>
            <td>Merit Health Central</td>
            <td>Jackson</td>
            <td>MS</td>
            <td>1108.0</td>
        </tr>
        <tr>
            <td>Memorial Hermann Northeast Hospital</td>
            <td>Humble</td>
            <td>TX</td>
            <td>1110.0</td>
        </tr>
        <tr>
            <td>Sterling Regional Medcenter</td>
            <td>Sterling</td>
            <td>CO</td>
            <td>1111.0</td>
        </tr>
        <tr>
            <td>Piedmont Newton Hospital</td>
            <td>Covington</td>
            <td>GA</td>
            <td>1112.0</td>
        </tr>
        <tr>
            <td>Colorado Plains Medical Center</td>
            <td>Fort Morgan</td>
            <td>CO</td>
            <td>1113.0</td>
        </tr>
        <tr>
            <td>Bourbon Community Hospital</td>
            <td>Paris</td>
            <td>KY</td>
            <td>1115.0</td>
        </tr>
        <tr>
            <td>Rolling Plains Memorial Hospital</td>
            <td>Sweetwater</td>
            <td>TX</td>
            <td>1116.0</td>
        </tr>
        <tr>
            <td>Desert Springs Hospital</td>
            <td>Las Vegas</td>
            <td>NV</td>
            <td>1117.0</td>
        </tr>
        <tr>
            <td>Roane Medical Center</td>
            <td>Harriman</td>
            <td>TN</td>
            <td>1118.0</td>
        </tr>
        <tr>
            <td>Ely Bloomenson Community Hospital</td>
            <td>Ely</td>
            <td>MN</td>
            <td>1119.0</td>
        </tr>
        <tr>
            <td>John D Archbold Memorial Hospital</td>
            <td>Thomasville</td>
            <td>GA</td>
            <td>1120.0</td>
        </tr>
        <tr>
            <td>Washington Health System Greene</td>
            <td>Waynesburg</td>
            <td>PA</td>
            <td>1121.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Carthage</td>
            <td>Carthage</td>
            <td>MO</td>
            <td>1122.0</td>
        </tr>
        <tr>
            <td>Gerald Champion Regional Medical Center</td>
            <td>Alamogordo</td>
            <td>NM</td>
            <td>1123.0</td>
        </tr>
        <tr>
            <td>Cape Fear Valley Medical Center</td>
            <td>Fayetteville</td>
            <td>NC</td>
            <td>1124.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Logan County</td>
            <td>Guthrie</td>
            <td>OK</td>
            <td>1125.0</td>
        </tr>
        <tr>
            <td>Saint Anthony Medical Center</td>
            <td>Rockford</td>
            <td>IL</td>
            <td>1126.0</td>
        </tr>
        <tr>
            <td>Baptist Memorial Hospital - Carroll County</td>
            <td>Huntingdon</td>
            <td>TN</td>
            <td>1127.0</td>
        </tr>
        <tr>
            <td>SSM Health St. Mary&#x27;s Hospital-Audrain</td>
            <td>Mexico</td>
            <td>MO</td>
            <td>1128.0</td>
        </tr>
        <tr>
            <td>St. Joseph&#x27;s Hospital Health Center</td>
            <td>Syracuse</td>
            <td>NY</td>
            <td>1129.0</td>
        </tr>
        <tr>
            <td>Hemet Valley Medical Center</td>
            <td>Hemet</td>
            <td>CA</td>
            <td>1130.0</td>
        </tr>
        <tr>
            <td>University Hospital and Medical Center</td>
            <td>Tamarac</td>
            <td>FL</td>
            <td>1131.0</td>
        </tr>
        <tr>
            <td>Newport Community Hospital</td>
            <td>Newport</td>
            <td>WA</td>
            <td>1132.0</td>
        </tr>
        <tr>
            <td>Morristown Hamblen Hospital Association</td>
            <td>Morristown</td>
            <td>TN</td>
            <td>1133.0</td>
        </tr>
        <tr>
            <td>Healdsburg Hospital</td>
            <td>Healdsburg</td>
            <td>CA</td>
            <td>1134.0</td>
        </tr>
        <tr>
            <td>Buchanan General Hospital</td>
            <td>Grundy</td>
            <td>VA</td>
            <td>1135.0</td>
        </tr>
        <tr>
            <td>Osceola Community Hospital</td>
            <td>Sibley</td>
            <td>IA</td>
            <td>1136.0</td>
        </tr>
        <tr>
            <td>CHI Health Missouri Valley</td>
            <td>Missouri Valley</td>
            <td>IA</td>
            <td>1137.0</td>
        </tr>
        <tr>
            <td>Firstlight Health System</td>
            <td>Mora</td>
            <td>MN</td>
            <td>1138.0</td>
        </tr>
        <tr>
            <td>Goshen General Hospital</td>
            <td>Goshen</td>
            <td>IN</td>
            <td>1139.0</td>
        </tr>
        <tr>
            <td>Wyckoff Heights Medical Center</td>
            <td>Brooklyn</td>
            <td>NY</td>
            <td>1141.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System - Waseca</td>
            <td>Waseca</td>
            <td>MN</td>
            <td>1142.0</td>
        </tr>
        <tr>
            <td>Christus Jasper Memorial Hospital</td>
            <td>Jasper</td>
            <td>TX</td>
            <td>1143.0</td>
        </tr>
        <tr>
            <td>John F Kennedy Memorial Hospital</td>
            <td>Indio</td>
            <td>CA</td>
            <td>1144.0</td>
        </tr>
        <tr>
            <td>Wilkes Regional Medical Center</td>
            <td>North Wilkesboro</td>
            <td>NC</td>
            <td>1145.0</td>
        </tr>
        <tr>
            <td>Leconte Medical Center</td>
            <td>Sevierville</td>
            <td>TN</td>
            <td>1146.0</td>
        </tr>
        <tr>
            <td>Greenfield Area Medical Center</td>
            <td>Greenfield</td>
            <td>OH</td>
            <td>1147.0</td>
        </tr>
        <tr>
            <td>CHI St. Alexius Health Devils Lake</td>
            <td>Devils Lake</td>
            <td>ND</td>
            <td>1148.0</td>
        </tr>
        <tr>
            <td>Nassau University Medical Center</td>
            <td>East Meadow</td>
            <td>NY</td>
            <td>1149.0</td>
        </tr>
        <tr>
            <td>Hendry Regional Medical Center</td>
            <td>Clewiston</td>
            <td>FL</td>
            <td>1150.0</td>
        </tr>
        <tr>
            <td>TMC - Bonham Hospital</td>
            <td>Bonham</td>
            <td>TX</td>
            <td>1151.0</td>
        </tr>
        <tr>
            <td>Southern Regional Medical Center</td>
            <td>Riverdale</td>
            <td>GA</td>
            <td>1152.0</td>
        </tr>
        <tr>
            <td>Marshall Medical Center</td>
            <td>Lewisburg</td>
            <td>TN</td>
            <td>1153.0</td>
        </tr>
        <tr>
            <td>Indiana Regional Medical Center</td>
            <td>Indiana</td>
            <td>PA</td>
            <td>1154.0</td>
        </tr>
        <tr>
            <td>Memorial Medical Center</td>
            <td>Springfield</td>
            <td>IL</td>
            <td>1155.0</td>
        </tr>
        <tr>
            <td>Valley Regional Hospital</td>
            <td>Claremont</td>
            <td>NH</td>
            <td>1156.0</td>
        </tr>
        <tr>
            <td>Glen Rose Medical Center</td>
            <td>Glen Rose</td>
            <td>TX</td>
            <td>1157.0</td>
        </tr>
        <tr>
            <td>Carilion Tazewell Community Hospital</td>
            <td>Tazewell</td>
            <td>VA</td>
            <td>1158.0</td>
        </tr>
        <tr>
            <td>Northern Montana Hospital</td>
            <td>Havre</td>
            <td>MT</td>
            <td>1159.0</td>
        </tr>
        <tr>
            <td>Delaware Valley Hospital</td>
            <td>Walton</td>
            <td>NY</td>
            <td>1161.0</td>
        </tr>
        <tr>
            <td>Bon Secours Richmond Community Hospital</td>
            <td>Richmond</td>
            <td>VA</td>
            <td>1162.0</td>
        </tr>
        <tr>
            <td>Capital Region Medical Center</td>
            <td>Jefferson City</td>
            <td>MO</td>
            <td>1163.0</td>
        </tr>
        <tr>
            <td>Ashtabula County Medical Center</td>
            <td>Ashtabula</td>
            <td>OH</td>
            <td>1164.0</td>
        </tr>
        <tr>
            <td>Stringfellow Memorial Hospital</td>
            <td>Anniston</td>
            <td>AL</td>
            <td>1165.0</td>
        </tr>
        <tr>
            <td>San Luis Valley Health</td>
            <td>Alamosa</td>
            <td>CO</td>
            <td>1166.0</td>
        </tr>
        <tr>
            <td>Sanford Vermillion Hospital</td>
            <td>Vermillion</td>
            <td>SD</td>
            <td>1167.0</td>
        </tr>
        <tr>
            <td>Dekalb Health</td>
            <td>Auburn</td>
            <td>IN</td>
            <td>1168.0</td>
        </tr>
        <tr>
            <td>Holy Cross Medical Center</td>
            <td>Taos</td>
            <td>NM</td>
            <td>1169.0</td>
        </tr>
        <tr>
            <td>Meeker Memorial Hospital</td>
            <td>Litchfield</td>
            <td>MN</td>
            <td>1170.0</td>
        </tr>
        <tr>
            <td>Spectrum Health Big Rapids Hospital</td>
            <td>Big Rapids</td>
            <td>MI</td>
            <td>1171.0</td>
        </tr>
        <tr>
            <td>Wagoner Community Hospital</td>
            <td>Wagoner</td>
            <td>OK</td>
            <td>1172.0</td>
        </tr>
        <tr>
            <td>Integris Miami Hospital</td>
            <td>Miami</td>
            <td>OK</td>
            <td>1173.0</td>
        </tr>
        <tr>
            <td>Abbeville Area Medical Center</td>
            <td>Abbeville</td>
            <td>SC</td>
            <td>1174.0</td>
        </tr>
        <tr>
            <td>ACMH Hospital</td>
            <td>Kittanning</td>
            <td>PA</td>
            <td>1175.0</td>
        </tr>
        <tr>
            <td>United Hospital District</td>
            <td>Blue Earth</td>
            <td>MN</td>
            <td>1177.0</td>
        </tr>
        <tr>
            <td>Community Regional Medical Center</td>
            <td>Fresno</td>
            <td>CA</td>
            <td>1178.0</td>
        </tr>
        <tr>
            <td>Broadlawns Medical Center</td>
            <td>Des Moines</td>
            <td>IA</td>
            <td>1179.0</td>
        </tr>
        <tr>
            <td>Vidant Edgecombe Hospital</td>
            <td>Tarboro</td>
            <td>NC</td>
            <td>1180.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Elmore Medical Center</td>
            <td>Mountain Home</td>
            <td>ID</td>
            <td>1181.0</td>
        </tr>
        <tr>
            <td>Decatur County Memorial Hospital</td>
            <td>Greensburg</td>
            <td>IN</td>
            <td>1182.0</td>
        </tr>
        <tr>
            <td>Modoc Medical Center</td>
            <td>Alturas</td>
            <td>CA</td>
            <td>1183.0</td>
        </tr>
        <tr>
            <td>Via Christi Hospital Pittsburg</td>
            <td>Pittsburg</td>
            <td>KS</td>
            <td>1185.0</td>
        </tr>
        <tr>
            <td>Ketchikan Medical Center</td>
            <td>Ketchikan</td>
            <td>AK</td>
            <td>1186.0</td>
        </tr>
        <tr>
            <td>Maricopa Medical Center</td>
            <td>Phoenix</td>
            <td>AZ</td>
            <td>1187.0</td>
        </tr>
        <tr>
            <td>Ochsner LSU Health Monroe</td>
            <td>Monroe</td>
            <td>LA</td>
            <td>1188.0</td>
        </tr>
        <tr>
            <td>St. Martin Hospital</td>
            <td>Breaux Bridge</td>
            <td>LA</td>
            <td>1189.0</td>
        </tr>
        <tr>
            <td>White Mountain Regional Medical Center</td>
            <td>Springerville</td>
            <td>AZ</td>
            <td>1190.0</td>
        </tr>
        <tr>
            <td>Crawford Memorial Hospital</td>
            <td>Robinson</td>
            <td>IL</td>
            <td>1191.0</td>
        </tr>
        <tr>
            <td>South Central Kansas Medical Center</td>
            <td>Arkansas City</td>
            <td>KS</td>
            <td>1192.0</td>
        </tr>
        <tr>
            <td>Adventist Health Tehachapi Valley</td>
            <td>Tehachapi</td>
            <td>CA</td>
            <td>1193.0</td>
        </tr>
        <tr>
            <td>Cassia Regional Hospital</td>
            <td>Burley</td>
            <td>ID</td>
            <td>1194.0</td>
        </tr>
        <tr>
            <td>Flambeau Hospital</td>
            <td>Park Falls</td>
            <td>WI</td>
            <td>1195.0</td>
        </tr>
        <tr>
            <td>Covenant Hospital Levelland</td>
            <td>Levelland</td>
            <td>TX</td>
            <td>1196.0</td>
        </tr>
        <tr>
            <td>Memorial Medical Center San Augustine</td>
            <td>San Augustine</td>
            <td>TX</td>
            <td>1197.0</td>
        </tr>
        <tr>
            <td>Humboldt General Hospital</td>
            <td>Winnemucca</td>
            <td>NV</td>
            <td>1199.0</td>
        </tr>
        <tr>
            <td>Sanford Sheldon Medical Center</td>
            <td>Sheldon</td>
            <td>IA</td>
            <td>1200.0</td>
        </tr>
        <tr>
            <td>St. John Sapulpa</td>
            <td>Sapulpa</td>
            <td>OK</td>
            <td>1201.0</td>
        </tr>
        <tr>
            <td>Tennova Healthcare-Lafollett Medical Center</td>
            <td>La Follette</td>
            <td>TN</td>
            <td>1202.0</td>
        </tr>
        <tr>
            <td>Carthage Area Hospital</td>
            <td>Carthage</td>
            <td>NY</td>
            <td>1203.0</td>
        </tr>
        <tr>
            <td>Midmichigan Medical Center-Clare</td>
            <td>Clare</td>
            <td>MI</td>
            <td>1204.0</td>
        </tr>
        <tr>
            <td>Marshall Browning Hospital</td>
            <td>Du Quoin</td>
            <td>IL</td>
            <td>1205.0</td>
        </tr>
        <tr>
            <td>Our Lady of the Angels Hospital</td>
            <td>Bogalusa</td>
            <td>LA</td>
            <td>1206.0</td>
        </tr>
        <tr>
            <td>Swisher Memorial Hospital</td>
            <td>Tulia</td>
            <td>TX</td>
            <td>1207.0</td>
        </tr>
        <tr>
            <td>Boone Memorial Hospital</td>
            <td>Madison</td>
            <td>WV</td>
            <td>1208.0</td>
        </tr>
        <tr>
            <td>Saint Francis Hospital Vinita</td>
            <td>Vinita</td>
            <td>OK</td>
            <td>1209.0</td>
        </tr>
        <tr>
            <td>Seymour Hospital</td>
            <td>Seymour</td>
            <td>TX</td>
            <td>1210.0</td>
        </tr>
        <tr>
            <td>Stones River Hospital</td>
            <td>Woodbury</td>
            <td>TN</td>
            <td>1211.0</td>
        </tr>
        <tr>
            <td>Christus Coushatta Health Care Center</td>
            <td>Coushatta</td>
            <td>LA</td>
            <td>1212.0</td>
        </tr>
        <tr>
            <td>Tyler County Hospital</td>
            <td>Woodville</td>
            <td>TX</td>
            <td>1213.0</td>
        </tr>
        <tr>
            <td>PeaceHealth Cottage Grove Community Medical Center</td>
            <td>Cottage Grove</td>
            <td>OR</td>
            <td>1214.0</td>
        </tr>
        <tr>
            <td>Hancock County Hospital</td>
            <td>Sneedville</td>
            <td>TN</td>
            <td>1215.0</td>
        </tr>
        <tr>
            <td>Northern Cochise Community Hospital.</td>
            <td>Willcox</td>
            <td>AZ</td>
            <td>1216.0</td>
        </tr>
        <tr>
            <td>Chi Memorial Hospital- Georgia</td>
            <td>Fort Oglethorpe</td>
            <td>GA</td>
            <td>1217.0</td>
        </tr>
        <tr>
            <td>LAC/Olive View-UCLA Medical Center</td>
            <td>Sylmar</td>
            <td>CA</td>
            <td>1218.0</td>
        </tr>
        <tr>
            <td>Truman Medical Center Hospital Hill</td>
            <td>Kansas City</td>
            <td>MO</td>
            <td>1219.0</td>
        </tr>
        <tr>
            <td>Zuckerberg San Francisco General Hosp &amp; Trauma Center</td>
            <td>San Francisco</td>
            <td>CA</td>
            <td>1220.0</td>
        </tr>
        <tr>
            <td>San Mateo Medical Center</td>
            <td>San Mateo</td>
            <td>CA</td>
            <td>1221.0</td>
        </tr>
        <tr>
            <td>John H. Stroger Jr. Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>1223.0</td>
        </tr>
        <tr>
            <td>Johns Hopkins Bayview Medical Center</td>
            <td>Baltimore</td>
            <td>MD</td>
            <td>1224.0</td>
        </tr>
        <tr>
            <td>NYC Health + Hospitals/Elmhurst</td>
            <td>Elmhurst</td>
            <td>NY</td>
            <td>1225.0</td>
        </tr>
        <tr>
            <td>Carepoint Health-Christ Hospital</td>
            <td>Jersey City</td>
            <td>NJ</td>
            <td>1226.0</td>
        </tr>
        <tr>
            <td>Howard University Hospital</td>
            <td>Washington</td>
            <td>DC</td>
            <td>1227.0</td>
        </tr>
        <tr>
            <td>Harborview Medical Center</td>
            <td>Seattle</td>
            <td>WA</td>
            <td>1229.0</td>
        </tr>
        <tr>
            <td>Community Hospital of San Bernardino</td>
            <td>San Bernardino</td>
            <td>CA</td>
            <td>1231.0</td>
        </tr>
        <tr>
            <td>Grady Memorial Hospital</td>
            <td>Atlanta</td>
            <td>GA</td>
            <td>1232.0</td>
        </tr>
        <tr>
            <td>Montefiore Medical Center</td>
            <td>Bronx</td>
            <td>NY</td>
            <td>1233.0</td>
        </tr>
        <tr>
            <td>Adventist Bolingbrook Hospital</td>
            <td>Bolingbrook</td>
            <td>IL</td>
            <td>1234.0</td>
        </tr>
        <tr>
            <td>Kern Medical Center</td>
            <td>Bakersfield</td>
            <td>CA</td>
            <td>1237.0</td>
        </tr>
        <tr>
            <td>Huntington Beach Hospital</td>
            <td>Huntington Beach</td>
            <td>CA</td>
            <td>1238.0</td>
        </tr>
        <tr>
            <td>Bellevue Hospital Center</td>
            <td>New York</td>
            <td>NY</td>
            <td>1239.0</td>
        </tr>
        <tr>
            <td>AllianceHealth Midwest</td>
            <td>Midwest City</td>
            <td>OK</td>
            <td>1241.0</td>
        </tr>
        <tr>
            <td>UNM Hospital</td>
            <td>Albuquerque</td>
            <td>NM</td>
            <td>1242.0</td>
        </tr>
        <tr>
            <td>Adventist Health Lodi Memorial</td>
            <td>Lodi</td>
            <td>CA</td>
            <td>1243.0</td>
        </tr>
        <tr>
            <td>St. Rose Hospital</td>
            <td>Hayward</td>
            <td>CA</td>
            <td>1244.0</td>
        </tr>
        <tr>
            <td>Harbor-UCLA Medical Center</td>
            <td>Torrance</td>
            <td>CA</td>
            <td>1245.0</td>
        </tr>
        <tr>
            <td>University of Louisville Hospital</td>
            <td>Louisville</td>
            <td>KY</td>
            <td>1246.0</td>
        </tr>
        <tr>
            <td>Baptist Memorial Hospital Desoto</td>
            <td>Southaven</td>
            <td>MS</td>
            <td>1247.0</td>
        </tr>
        <tr>
            <td>University Hospital of Brooklyn ( Downstate )</td>
            <td>Brooklyn</td>
            <td>NY</td>
            <td>1248.0</td>
        </tr>
        <tr>
            <td>Detroit Receiving Hospital &amp; University Health Center</td>
            <td>Detroit</td>
            <td>MI</td>
            <td>1249.0</td>
        </tr>
        <tr>
            <td>Eastern Niagara Hospital</td>
            <td>Lockport</td>
            <td>NY</td>
            <td>1250.0</td>
        </tr>
        <tr>
            <td>Hillcrest Hospital Cushing</td>
            <td>Cushing</td>
            <td>OK</td>
            <td>1251.0</td>
        </tr>
        <tr>
            <td>St. John&#x27;s Health</td>
            <td>Jackson</td>
            <td>WY</td>
            <td>1252.0</td>
        </tr>
        <tr>
            <td>Mills-Peninsula Medical Center</td>
            <td>Burlingame</td>
            <td>CA</td>
            <td>1253.0</td>
        </tr>
        <tr>
            <td>St. Vincent Fishers Hospital</td>
            <td>Fishers</td>
            <td>IN</td>
            <td>1254.0</td>
        </tr>
        <tr>
            <td>Sheridan Memorial Hospital</td>
            <td>Sheridan</td>
            <td>WY</td>
            <td>1255.0</td>
        </tr>
        <tr>
            <td>Baptist Health La Grange</td>
            <td>La Grange</td>
            <td>KY</td>
            <td>1256.0</td>
        </tr>
        <tr>
            <td>Schneck Medical Center</td>
            <td>Seymour</td>
            <td>IN</td>
            <td>1257.0</td>
        </tr>
        <tr>
            <td>Aspen Valley Hospital</td>
            <td>Aspen</td>
            <td>CO</td>
            <td>1259.0</td>
        </tr>
        <tr>
            <td>Fostoria Community Hospital</td>
            <td>Fostoria</td>
            <td>OH</td>
            <td>1260.0</td>
        </tr>
        <tr>
            <td>Lahey Hospital &amp; Medical Center, Burlington</td>
            <td>Burlington</td>
            <td>MA</td>
            <td>1261.0</td>
        </tr>
        <tr>
            <td>Sutter Tracy Community Hospital</td>
            <td>Tracy</td>
            <td>CA</td>
            <td>1262.0</td>
        </tr>
        <tr>
            <td>Mercy Health - Defiance Hospital</td>
            <td>Defiance</td>
            <td>OH</td>
            <td>1263.0</td>
        </tr>
        <tr>
            <td>Shenandoah Memorial Hospital</td>
            <td>Woodstock</td>
            <td>VA</td>
            <td>1264.0</td>
        </tr>
        <tr>
            <td>Northfield Hospital</td>
            <td>Northfield</td>
            <td>MN</td>
            <td>1265.0</td>
        </tr>
        <tr>
            <td>District One Hospital</td>
            <td>Faribault</td>
            <td>MN</td>
            <td>1266.0</td>
        </tr>
        <tr>
            <td>CHI Health St. Francis</td>
            <td>Grand Island</td>
            <td>NE</td>
            <td>1267.0</td>
        </tr>
        <tr>
            <td>Gulf Coast Medical Center Lee Memorial Health System</td>
            <td>Fort Myers</td>
            <td>FL</td>
            <td>1268.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic</td>
            <td>Jacksonville</td>
            <td>FL</td>
            <td>1269.0</td>
        </tr>
        <tr>
            <td>Bingham Memorial Hospital</td>
            <td>Blackfoot</td>
            <td>ID</td>
            <td>1270.0</td>
        </tr>
        <tr>
            <td>Stormont Vail Hospital</td>
            <td>Topeka</td>
            <td>KS</td>
            <td>1271.0</td>
        </tr>
        <tr>
            <td>Ascension Columbia St. Mary&#x27;s Hospital Ozaukee</td>
            <td>Mequon</td>
            <td>WI</td>
            <td>1272.0</td>
        </tr>
        <tr>
            <td>Faith Regional Health Services</td>
            <td>Norfolk</td>
            <td>NE</td>
            <td>1273.0</td>
        </tr>
        <tr>
            <td>Lone Peak Hospital</td>
            <td>Draper</td>
            <td>UT</td>
            <td>1274.0</td>
        </tr>
        <tr>
            <td>Pratt Regional Medical Center</td>
            <td>Pratt</td>
            <td>KS</td>
            <td>1275.0</td>
        </tr>
        <tr>
            <td>Sentara Princess Anne Hospital</td>
            <td>Virginia Beach</td>
            <td>VA</td>
            <td>1276.0</td>
        </tr>
        <tr>
            <td>El Camino Hospital</td>
            <td>Mountain View</td>
            <td>CA</td>
            <td>1277.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital St. Louis</td>
            <td>Saint Louis</td>
            <td>MO</td>
            <td>1278.0</td>
        </tr>
        <tr>
            <td>Duke Health Raleigh Hospital</td>
            <td>Raleigh</td>
            <td>NC</td>
            <td>1280.0</td>
        </tr>
        <tr>
            <td>UPMC Passavant</td>
            <td>Pittsburgh</td>
            <td>PA</td>
            <td>1281.0</td>
        </tr>
        <tr>
            <td>St. Joseph&#x27;s Hospital and Medical Center</td>
            <td>Phoenix</td>
            <td>AZ</td>
            <td>1282.0</td>
        </tr>
        <tr>
            <td>University of Wisconsin Hospitals &amp; Clinics</td>
            <td>Madison</td>
            <td>WI</td>
            <td>1283.0</td>
        </tr>
        <tr>
            <td>Riverside Tappahannock Hospital</td>
            <td>Tappahannock</td>
            <td>VA</td>
            <td>1284.0</td>
        </tr>
        <tr>
            <td>Salem Regional Medical Center</td>
            <td>Salem</td>
            <td>OH</td>
            <td>1285.0</td>
        </tr>
        <tr>
            <td>St. Vincent Hospital &amp; Health Services</td>
            <td>Indianapolis</td>
            <td>IN</td>
            <td>1286.0</td>
        </tr>
        <tr>
            <td>Advocate Good Shepherd Hospital</td>
            <td>Barrington</td>
            <td>IL</td>
            <td>1287.0</td>
        </tr>
        <tr>
            <td>Howard Young Medical Center</td>
            <td>Woodruff</td>
            <td>WI</td>
            <td>1288.0</td>
        </tr>
        <tr>
            <td>Owatonna Hospital</td>
            <td>Owatonna</td>
            <td>MN</td>
            <td>1289.0</td>
        </tr>
        <tr>
            <td>Reid Health</td>
            <td>Richmond</td>
            <td>IN</td>
            <td>1290.0</td>
        </tr>
        <tr>
            <td>Emory Johns Creek Hospital</td>
            <td>Johns Creek</td>
            <td>GA</td>
            <td>1291.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Hospital</td>
            <td>Phoenix</td>
            <td>AZ</td>
            <td>1292.0</td>
        </tr>
        <tr>
            <td>Stanford Health Care</td>
            <td>Stanford</td>
            <td>CA</td>
            <td>1293.0</td>
        </tr>
        <tr>
            <td>Swedish Issaquah</td>
            <td>Issaquah</td>
            <td>WA</td>
            <td>1294.0</td>
        </tr>
        <tr>
            <td>Saint Joseph Hospital</td>
            <td>Lexington</td>
            <td>KY</td>
            <td>1295.0</td>
        </tr>
        <tr>
            <td>Eastern Idaho Regional Medical Center</td>
            <td>Idaho Falls</td>
            <td>ID</td>
            <td>1296.0</td>
        </tr>
        <tr>
            <td>United Regional Health Care System</td>
            <td>Wichita Falls</td>
            <td>TX</td>
            <td>1297.0</td>
        </tr>
        <tr>
            <td>Cheyenne Regional Medical Center</td>
            <td>Cheyenne</td>
            <td>WY</td>
            <td>1298.0</td>
        </tr>
        <tr>
            <td>Advocate Bromenn Medical Center</td>
            <td>Normal</td>
            <td>IL</td>
            <td>1299.0</td>
        </tr>
        <tr>
            <td>Healtheast St. John&#x27;s Hospital</td>
            <td>Maplewood</td>
            <td>MN</td>
            <td>1300.0</td>
        </tr>
        <tr>
            <td>UT Southwestern University Hospital</td>
            <td>Dallas</td>
            <td>TX</td>
            <td>1301.0</td>
        </tr>
        <tr>
            <td>Meadowview Regional Medical Center</td>
            <td>Maysville</td>
            <td>KY</td>
            <td>1302.0</td>
        </tr>
        <tr>
            <td>Verde Valley Medical Center</td>
            <td>Cottonwood</td>
            <td>AZ</td>
            <td>1303.0</td>
        </tr>
        <tr>
            <td>University Hospitals - Elyria Medical Center</td>
            <td>Elyria</td>
            <td>OH</td>
            <td>1304.0</td>
        </tr>
        <tr>
            <td>Blanchard Valley Hospital</td>
            <td>Findlay</td>
            <td>OH</td>
            <td>1305.0</td>
        </tr>
        <tr>
            <td>CHI Health Lakeside</td>
            <td>Omaha</td>
            <td>NE</td>
            <td>1306.0</td>
        </tr>
        <tr>
            <td>Wise Regional Health System</td>
            <td>Decatur</td>
            <td>TX</td>
            <td>1307.0</td>
        </tr>
        <tr>
            <td>North Ottawa Community Health System</td>
            <td>Grand Haven</td>
            <td>MI</td>
            <td>1309.0</td>
        </tr>
        <tr>
            <td>Genesys Regional Medical Center - Health Park</td>
            <td>Grand Blanc</td>
            <td>MI</td>
            <td>1310.0</td>
        </tr>
        <tr>
            <td>Overlake Hospital Medical Center</td>
            <td>Bellevue</td>
            <td>WA</td>
            <td>1311.0</td>
        </tr>
        <tr>
            <td>Baptist Health Lexington</td>
            <td>Lexington</td>
            <td>KY</td>
            <td>1312.0</td>
        </tr>
        <tr>
            <td>Morristown Medical Center</td>
            <td>Morristown</td>
            <td>NJ</td>
            <td>1313.0</td>
        </tr>
        <tr>
            <td>Piedmont Newnan Hospital</td>
            <td>Newnan</td>
            <td>GA</td>
            <td>1314.0</td>
        </tr>
        <tr>
            <td>Henrico Doctors&#x27; Hospital</td>
            <td>Richmond</td>
            <td>VA</td>
            <td>1315.0</td>
        </tr>
        <tr>
            <td>Artesia General Hospital</td>
            <td>Artesia</td>
            <td>NM</td>
            <td>1316.0</td>
        </tr>
        <tr>
            <td>Baptist St. Anthony&#x27;s Hospital</td>
            <td>Amarillo</td>
            <td>TX</td>
            <td>1317.0</td>
        </tr>
        <tr>
            <td>Medical City Weatherford</td>
            <td>Weatherford</td>
            <td>TX</td>
            <td>1318.0</td>
        </tr>
        <tr>
            <td>Cape Canaveral Hospital</td>
            <td>Cocoa Beach</td>
            <td>FL</td>
            <td>1319.0</td>
        </tr>
        <tr>
            <td>UHHS Richmond Heights Hospital</td>
            <td>Richmond Heights</td>
            <td>OH</td>
            <td>1320.0</td>
        </tr>
        <tr>
            <td>GHS Oconee MemorialÂ¬â€ Hospital</td>
            <td>Seneca</td>
            <td>SC</td>
            <td>1321.0</td>
        </tr>
        <tr>
            <td>Columbus Community Hospital</td>
            <td>Columbus</td>
            <td>NE</td>
            <td>1322.0</td>
        </tr>
        <tr>
            <td>Aurora Medical Center Washington County</td>
            <td>Hartford</td>
            <td>WI</td>
            <td>1323.0</td>
        </tr>
        <tr>
            <td>Swedish Covenant Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>1324.0</td>
        </tr>
        <tr>
            <td>Main Line Health- Paoli Hospital</td>
            <td>Paoli</td>
            <td>PA</td>
            <td>1325.0</td>
        </tr>
        <tr>
            <td>Gulf Breeze Hospital</td>
            <td>Gulf Breeze</td>
            <td>FL</td>
            <td>1326.0</td>
        </tr>
        <tr>
            <td>Nason Medical Center</td>
            <td>Roaring Spring</td>
            <td>PA</td>
            <td>1328.0</td>
        </tr>
        <tr>
            <td>Parma Community General Hospital</td>
            <td>Parma</td>
            <td>OH</td>
            <td>1329.0</td>
        </tr>
        <tr>
            <td>Delnor Community Hospital</td>
            <td>Geneva</td>
            <td>IL</td>
            <td>1331.0</td>
        </tr>
        <tr>
            <td>United Hospital Center</td>
            <td>Bridgeport</td>
            <td>WV</td>
            <td>1332.0</td>
        </tr>
        <tr>
            <td>Prisma Health Baptist Parkridge</td>
            <td>Columbia</td>
            <td>SC</td>
            <td>1333.0</td>
        </tr>
        <tr>
            <td>Metroplex Hospital</td>
            <td>Killeen</td>
            <td>TX</td>
            <td>1334.0</td>
        </tr>
        <tr>
            <td>Howard County General Hospital</td>
            <td>Columbia</td>
            <td>MD</td>
            <td>1335.0</td>
        </tr>
        <tr>
            <td>Virginia Hospital Center</td>
            <td>Arlington</td>
            <td>VA</td>
            <td>1336.0</td>
        </tr>
        <tr>
            <td>Northwest Medical Center-Springdale</td>
            <td>Springdale</td>
            <td>AR</td>
            <td>1337.0</td>
        </tr>
        <tr>
            <td>Abrazo West Campus</td>
            <td>Goodyear</td>
            <td>AZ</td>
            <td>1338.0</td>
        </tr>
        <tr>
            <td>Overlook Medical Center</td>
            <td>Summit</td>
            <td>NJ</td>
            <td>1339.0</td>
        </tr>
        <tr>
            <td>Sarasota Memorial Hospital</td>
            <td>Sarasota</td>
            <td>FL</td>
            <td>1342.0</td>
        </tr>
        <tr>
            <td>Prisma Health Baptist</td>
            <td>Columbia</td>
            <td>SC</td>
            <td>1343.0</td>
        </tr>
        <tr>
            <td>Lourdes Hospital</td>
            <td>Paducah</td>
            <td>KY</td>
            <td>1344.0</td>
        </tr>
        <tr>
            <td>Houston Methodist Willowbrook Hospital</td>
            <td>Houston</td>
            <td>TX</td>
            <td>1345.0</td>
        </tr>
        <tr>
            <td>Mission Hospital Regional Medical Center</td>
            <td>Mission Viejo</td>
            <td>CA</td>
            <td>1346.0</td>
        </tr>
        <tr>
            <td>St. Francis Hospital, Roslyn</td>
            <td>Roslyn</td>
            <td>NY</td>
            <td>1347.0</td>
        </tr>
        <tr>
            <td>Scottsdale Thompson Peak Medical Center</td>
            <td>Scottsdale</td>
            <td>AZ</td>
            <td>1348.0</td>
        </tr>
        <tr>
            <td>Silver Cross HospitalÂ¬â€  and Medical Centers</td>
            <td>New Lenox</td>
            <td>IL</td>
            <td>1350.0</td>
        </tr>
        <tr>
            <td>Sky Ridge Medical Center</td>
            <td>Lone Tree</td>
            <td>CO</td>
            <td>1351.0</td>
        </tr>
        <tr>
            <td>Riverside Medical Center</td>
            <td>Kankakee</td>
            <td>IL</td>
            <td>1352.0</td>
        </tr>
        <tr>
            <td>Lewisgale Hospital Alleghany</td>
            <td>Low Moor</td>
            <td>VA</td>
            <td>1353.0</td>
        </tr>
        <tr>
            <td>Novant Health UVA Health Haymarket Medical Center</td>
            <td>Haymarket</td>
            <td>VA</td>
            <td>1354.0</td>
        </tr>
        <tr>
            <td>Banner Boswell Medical Center</td>
            <td>Sun City</td>
            <td>AZ</td>
            <td>1355.0</td>
        </tr>
        <tr>
            <td>Northside Hospital Cherokee</td>
            <td>Canton</td>
            <td>GA</td>
            <td>1356.0</td>
        </tr>
        <tr>
            <td>Hilton Head Regional Medical Center</td>
            <td>Hilton Head Island</td>
            <td>SC</td>
            <td>1357.0</td>
        </tr>
        <tr>
            <td>Chester County Hospital</td>
            <td>West Chester</td>
            <td>PA</td>
            <td>1358.0</td>
        </tr>
        <tr>
            <td>Evanston Hospital</td>
            <td>Evanston</td>
            <td>IL</td>
            <td>1359.0</td>
        </tr>
        <tr>
            <td>Dublin Methodist Hospital</td>
            <td>Dublin</td>
            <td>OH</td>
            <td>1360.0</td>
        </tr>
        <tr>
            <td>Henry Ford West Bloomfield Hospital</td>
            <td>West Bloomfield</td>
            <td>MI</td>
            <td>1361.0</td>
        </tr>
        <tr>
            <td>Washington Regional Medical Center</td>
            <td>Fayetteville</td>
            <td>AR</td>
            <td>1362.0</td>
        </tr>
        <tr>
            <td>Mercy Health-St. Rita&#x27;s Medical Center</td>
            <td>Lima</td>
            <td>OH</td>
            <td>1363.0</td>
        </tr>
        <tr>
            <td>Holy Cross Hospital</td>
            <td>Fort Lauderdale</td>
            <td>FL</td>
            <td>1364.0</td>
        </tr>
        <tr>
            <td>Mount Nittany Medical Center</td>
            <td>State College</td>
            <td>PA</td>
            <td>1365.0</td>
        </tr>
        <tr>
            <td>Harlingen Medical Center</td>
            <td>Harlingen</td>
            <td>TX</td>
            <td>1366.0</td>
        </tr>
        <tr>
            <td>Doctors Hospital of Laredo</td>
            <td>Laredo</td>
            <td>TX</td>
            <td>1367.0</td>
        </tr>
        <tr>
            <td>Northern Dutchess Hospital</td>
            <td>Rhinebeck</td>
            <td>NY</td>
            <td>1368.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s the Woodlands Hospital</td>
            <td>The Woodlands</td>
            <td>TX</td>
            <td>1369.0</td>
        </tr>
        <tr>
            <td>Palmetto Health Richland</td>
            <td>Columbia</td>
            <td>SC</td>
            <td>1370.0</td>
        </tr>
        <tr>
            <td>Jane Phillips Memorial Medical Center</td>
            <td>Bartlesville</td>
            <td>OK</td>
            <td>1371.0</td>
        </tr>
        <tr>
            <td>Eisenhower Medical Center</td>
            <td>Rancho Mirage</td>
            <td>CA</td>
            <td>1372.0</td>
        </tr>
        <tr>
            <td>Novant Health Matthews Medical Center</td>
            <td>Matthews</td>
            <td>NC</td>
            <td>1373.0</td>
        </tr>
        <tr>
            <td>Kishwaukee Community Hospital</td>
            <td>Dekalb</td>
            <td>IL</td>
            <td>1374.0</td>
        </tr>
        <tr>
            <td>Bon Secours St. Francis Medical Center</td>
            <td>Midlothian</td>
            <td>VA</td>
            <td>1375.0</td>
        </tr>
        <tr>
            <td>Geisinger-Community Medical Center</td>
            <td>Scranton</td>
            <td>PA</td>
            <td>1376.0</td>
        </tr>
        <tr>
            <td>John C. Lincoln North Mountain Hospital</td>
            <td>Phoenix</td>
            <td>AZ</td>
            <td>1377.0</td>
        </tr>
        <tr>
            <td>John Muir Medical Center - Walnut Creek Campus</td>
            <td>Walnut Creek</td>
            <td>CA</td>
            <td>1378.0</td>
        </tr>
        <tr>
            <td>Owensboro Health Regional Hospital</td>
            <td>Owensboro</td>
            <td>KY</td>
            <td>1379.0</td>
        </tr>
        <tr>
            <td>Scripps Memorial Hospital La Jolla</td>
            <td>La Jolla</td>
            <td>CA</td>
            <td>1380.0</td>
        </tr>
        <tr>
            <td>St. John Medical Center</td>
            <td>Westlake</td>
            <td>OH</td>
            <td>1381.0</td>
        </tr>
        <tr>
            <td>Wood County Hospital</td>
            <td>Bowling Green</td>
            <td>OH</td>
            <td>1382.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Fort Smith</td>
            <td>Fort Smith</td>
            <td>AR</td>
            <td>1383.0</td>
        </tr>
        <tr>
            <td>Southern Hills Hospital and Medical Center</td>
            <td>Las Vegas</td>
            <td>NV</td>
            <td>1384.0</td>
        </tr>
        <tr>
            <td>Beaumont Hospital, Royal Oak</td>
            <td>Royal Oak</td>
            <td>MI</td>
            <td>1385.0</td>
        </tr>
        <tr>
            <td>University of MD Upper Chesapeake Medical Center</td>
            <td>Bel Air</td>
            <td>MD</td>
            <td>1386.0</td>
        </tr>
        <tr>
            <td>Western Reserve Hospital</td>
            <td>Cuyahoga Falls</td>
            <td>OH</td>
            <td>1387.0</td>
        </tr>
        <tr>
            <td>Campbell County Memorial Hospital</td>
            <td>Gillette</td>
            <td>WY</td>
            <td>1388.0</td>
        </tr>
        <tr>
            <td>Englewood Community Hospital</td>
            <td>Englewood</td>
            <td>FL</td>
            <td>1389.0</td>
        </tr>
        <tr>
            <td>Ascension Via Christi Hospital St. Teresa</td>
            <td>Wichita</td>
            <td>KS</td>
            <td>1390.0</td>
        </tr>
        <tr>
            <td>Texas Health Presbyterian HospitalÂ¬â€ Dallas</td>
            <td>Dallas</td>
            <td>TX</td>
            <td>1391.0</td>
        </tr>
        <tr>
            <td>Oconomowoc Memorial Hospital</td>
            <td>Oconomowoc</td>
            <td>WI</td>
            <td>1392.0</td>
        </tr>
        <tr>
            <td>Jersey Shore University Medical Center</td>
            <td>Neptune</td>
            <td>NJ</td>
            <td>1393.0</td>
        </tr>
        <tr>
            <td>Watauga Medical Center</td>
            <td>Boone</td>
            <td>NC</td>
            <td>1394.0</td>
        </tr>
        <tr>
            <td>Tucson Medical Center</td>
            <td>Tucson</td>
            <td>AZ</td>
            <td>1395.0</td>
        </tr>
        <tr>
            <td>South County Hospital</td>
            <td>Wakefield</td>
            <td>RI</td>
            <td>1396.0</td>
        </tr>
        <tr>
            <td>Main Line Health- Lankenau Medical Center</td>
            <td>Wynnewood</td>
            <td>PA</td>
            <td>1397.0</td>
        </tr>
        <tr>
            <td>Canyon Vista Medical Center</td>
            <td>Sierra Vista</td>
            <td>AZ</td>
            <td>1398.0</td>
        </tr>
        <tr>
            <td>Virtua West Jersey Hospitals Voorhees</td>
            <td>Voorhees</td>
            <td>NJ</td>
            <td>1399.0</td>
        </tr>
        <tr>
            <td>Advocate Good Samaritan Hospital</td>
            <td>Downers Grove</td>
            <td>IL</td>
            <td>1400.0</td>
        </tr>
        <tr>
            <td>Missouri Baptist Medical Center</td>
            <td>Town And Country</td>
            <td>MO</td>
            <td>1401.0</td>
        </tr>
        <tr>
            <td>Memorialcare Saddleback Medical Center</td>
            <td>Laguna Hills</td>
            <td>CA</td>
            <td>1402.0</td>
        </tr>
        <tr>
            <td>Memorial Hermann Memorial City Medical Center</td>
            <td>Houston</td>
            <td>TX</td>
            <td>1403.0</td>
        </tr>
        <tr>
            <td>AdventHealth Daytona Beach</td>
            <td>Daytona Beach</td>
            <td>FL</td>
            <td>1404.0</td>
        </tr>
        <tr>
            <td>Penn Medicine Princeton Medical Center</td>
            <td>Plainsboro</td>
            <td>NJ</td>
            <td>1405.0</td>
        </tr>
        <tr>
            <td>Christus St. Michael Health System</td>
            <td>Texarkana</td>
            <td>TX</td>
            <td>1406.0</td>
        </tr>
        <tr>
            <td>St. Vincent&#x27;s Birmingham</td>
            <td>Birmingham</td>
            <td>AL</td>
            <td>1407.0</td>
        </tr>
        <tr>
            <td>Northwestern Memorial Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>1408.0</td>
        </tr>
        <tr>
            <td>HonorHealth Deer Valley Medical Center</td>
            <td>Phoenix</td>
            <td>AZ</td>
            <td>1409.0</td>
        </tr>
        <tr>
            <td>Houston Methodist West Hospital</td>
            <td>Houston</td>
            <td>TX</td>
            <td>1410.0</td>
        </tr>
        <tr>
            <td>Texas Health Presbyterian Hospital Flower Mound</td>
            <td>Flower Mound</td>
            <td>TX</td>
            <td>1411.0</td>
        </tr>
        <tr>
            <td>AdventHealth Orlando</td>
            <td>Orlando</td>
            <td>FL</td>
            <td>1412.0</td>
        </tr>
        <tr>
            <td>Northeast Regional Medical Center</td>
            <td>Kirksville</td>
            <td>MO</td>
            <td>1413.0</td>
        </tr>
        <tr>
            <td>Emerson Hospital</td>
            <td>W Concord</td>
            <td>MA</td>
            <td>1414.0</td>
        </tr>
        <tr>
            <td>Baptist Memorial Hospital Union City</td>
            <td>Union City</td>
            <td>TN</td>
            <td>1415.0</td>
        </tr>
        <tr>
            <td>Texas Health Arlington Memorial Hospital</td>
            <td>Arlington</td>
            <td>TX</td>
            <td>1416.0</td>
        </tr>
        <tr>
            <td>Grand Lake Health System</td>
            <td>Saint Marys</td>
            <td>OH</td>
            <td>1418.0</td>
        </tr>
        <tr>
            <td>East Jefferson General Hospital</td>
            <td>Metairie</td>
            <td>LA</td>
            <td>1419.0</td>
        </tr>
        <tr>
            <td>Centura Health-Littleton Adventist Hospital</td>
            <td>Littleton</td>
            <td>CO</td>
            <td>1420.0</td>
        </tr>
        <tr>
            <td>Christus Ochsner St. Patrick Hospital</td>
            <td>Lake Charles</td>
            <td>LA</td>
            <td>1421.0</td>
        </tr>
        <tr>
            <td>Menorah Medical Center</td>
            <td>Overland Park</td>
            <td>KS</td>
            <td>1422.0</td>
        </tr>
        <tr>
            <td>Kingman Regional Medical Center</td>
            <td>Kingman</td>
            <td>AZ</td>
            <td>1423.0</td>
        </tr>
        <tr>
            <td>Halifax Health Medical Center</td>
            <td>Daytona Beach</td>
            <td>FL</td>
            <td>1424.0</td>
        </tr>
        <tr>
            <td>Houston Methodist St. John Hospital</td>
            <td>Nassau Bay</td>
            <td>TX</td>
            <td>1425.0</td>
        </tr>
        <tr>
            <td>Nanticoke Memorial Hospital</td>
            <td>Seaford</td>
            <td>DE</td>
            <td>1426.0</td>
        </tr>
        <tr>
            <td>Aurora Medical Center Summit</td>
            <td>Summit</td>
            <td>WI</td>
            <td>1427.0</td>
        </tr>
        <tr>
            <td>Marin General Hospital</td>
            <td>Greenbrae</td>
            <td>CA</td>
            <td>1428.0</td>
        </tr>
        <tr>
            <td>Texas Health Presbyterian Hospital Rockwall</td>
            <td>Rockwall</td>
            <td>TX</td>
            <td>1429.0</td>
        </tr>
        <tr>
            <td>Hillcrest Hospital</td>
            <td>Mayfield Heights</td>
            <td>OH</td>
            <td>1430.0</td>
        </tr>
        <tr>
            <td>Adventist Hinsdale Hospital</td>
            <td>Hinsdale</td>
            <td>IL</td>
            <td>1431.0</td>
        </tr>
        <tr>
            <td>University Hospitals Ahuja Medical Center</td>
            <td>Beachwood</td>
            <td>OH</td>
            <td>1432.0</td>
        </tr>
        <tr>
            <td>South Bay Hospital</td>
            <td>Sun City Center</td>
            <td>FL</td>
            <td>1433.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Oklahoma City</td>
            <td>Oklahoma City</td>
            <td>OK</td>
            <td>1435.0</td>
        </tr>
        <tr>
            <td>Steward Melbourne Hospital</td>
            <td>Melbourne</td>
            <td>FL</td>
            <td>1436.0</td>
        </tr>
        <tr>
            <td>Franciscan Health Dyer</td>
            <td>Dyer</td>
            <td>IN</td>
            <td>1437.0</td>
        </tr>
        <tr>
            <td>Banner Del E. Webb Medical Center</td>
            <td>Sun City West</td>
            <td>AZ</td>
            <td>1438.0</td>
        </tr>
        <tr>
            <td>Physicians Regional Medical Center - Pine Ridge</td>
            <td>Naples</td>
            <td>FL</td>
            <td>1439.0</td>
        </tr>
        <tr>
            <td>Newton-Wellesley Hospital</td>
            <td>Newton</td>
            <td>MA</td>
            <td>1440.0</td>
        </tr>
        <tr>
            <td>Redlands Community Hospital</td>
            <td>Redlands</td>
            <td>CA</td>
            <td>1441.0</td>
        </tr>
        <tr>
            <td>Hoag Memorial Hospital Presbyterian</td>
            <td>Newport Beach</td>
            <td>CA</td>
            <td>1442.0</td>
        </tr>
        <tr>
            <td>Houston Medical Center</td>
            <td>Warner Robins</td>
            <td>GA</td>
            <td>1443.0</td>
        </tr>
        <tr>
            <td>Kettering Medical Center</td>
            <td>Kettering</td>
            <td>OH</td>
            <td>1444.0</td>
        </tr>
        <tr>
            <td>Boulder Community Health</td>
            <td>Boulder</td>
            <td>CO</td>
            <td>1445.0</td>
        </tr>
        <tr>
            <td>Portsmouth Regional Hospital</td>
            <td>Portsmouth</td>
            <td>NH</td>
            <td>1446.0</td>
        </tr>
        <tr>
            <td>Stamford Hospital</td>
            <td>Stamford</td>
            <td>CT</td>
            <td>1447.0</td>
        </tr>
        <tr>
            <td>Putnam Hospital Center</td>
            <td>Carmel</td>
            <td>NY</td>
            <td>1448.0</td>
        </tr>
        <tr>
            <td>Jupiter Medical Center</td>
            <td>Jupiter</td>
            <td>FL</td>
            <td>1449.0</td>
        </tr>
        <tr>
            <td>Wythe County Community Hospital</td>
            <td>Wytheville</td>
            <td>VA</td>
            <td>1450.0</td>
        </tr>
        <tr>
            <td>Huron Valley-Sinai Hospital</td>
            <td>Commerce Township</td>
            <td>MI</td>
            <td>1451.0</td>
        </tr>
        <tr>
            <td>Houston Methodist Sugarland Hospital</td>
            <td>Sugar Land</td>
            <td>TX</td>
            <td>1452.0</td>
        </tr>
        <tr>
            <td>Mountain Vista Medical Center</td>
            <td>Mesa</td>
            <td>AZ</td>
            <td>1453.0</td>
        </tr>
        <tr>
            <td>Presence Saint Joseph Hospital - Chicago</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>1454.0</td>
        </tr>
        <tr>
            <td>Baptist Medical Center - Beaches</td>
            <td>Jacksonville Beach</td>
            <td>FL</td>
            <td>1455.0</td>
        </tr>
        <tr>
            <td>Grandview Medical Center</td>
            <td>Birmingham</td>
            <td>AL</td>
            <td>1456.0</td>
        </tr>
        <tr>
            <td>Cleveland Clinic Indian River Hospital</td>
            <td>Vero Beach</td>
            <td>FL</td>
            <td>1457.0</td>
        </tr>
        <tr>
            <td>Beaumont Hospital - Trenton</td>
            <td>Trenton</td>
            <td>MI</td>
            <td>1458.0</td>
        </tr>
        <tr>
            <td>Edward Hospital</td>
            <td>Naperville</td>
            <td>IL</td>
            <td>1459.0</td>
        </tr>
        <tr>
            <td>Valley Hospital</td>
            <td>Ridgewood</td>
            <td>NJ</td>
            <td>1460.0</td>
        </tr>
        <tr>
            <td>Baylor Scott &amp; White Medical CenterÂ¬â€ Grapevine</td>
            <td>Grapevine</td>
            <td>TX</td>
            <td>1461.0</td>
        </tr>
        <tr>
            <td>Los Robles Hospital &amp; Medical Center</td>
            <td>Thousand Oaks</td>
            <td>CA</td>
            <td>1462.0</td>
        </tr>
        <tr>
            <td>St. Clair Hospital</td>
            <td>Pittsburgh</td>
            <td>PA</td>
            <td>1463.0</td>
        </tr>
        <tr>
            <td>Detar Healthcare System</td>
            <td>Victoria</td>
            <td>TX</td>
            <td>1464.0</td>
        </tr>
        <tr>
            <td>Torrance Memorial Medical Center</td>
            <td>Torrance</td>
            <td>CA</td>
            <td>1465.0</td>
        </tr>
        <tr>
            <td>Carepoint Health - Bayonne Medical Center</td>
            <td>Bayonne</td>
            <td>NJ</td>
            <td>1466.0</td>
        </tr>
        <tr>
            <td>Scottsdale Osborn Medical Center</td>
            <td>Scottsdale</td>
            <td>AZ</td>
            <td>1467.0</td>
        </tr>
        <tr>
            <td>Bakersfield Heart Hospital</td>
            <td>Bakersfield</td>
            <td>CA</td>
            <td>1468.0</td>
        </tr>
        <tr>
            <td>Resolute Health Hospital</td>
            <td>New Braunfels</td>
            <td>TX</td>
            <td>1469.0</td>
        </tr>
        <tr>
            <td>Tennova Healthcare-Jefferson Memorial Hospital</td>
            <td>Jefferson City</td>
            <td>TN</td>
            <td>1470.0</td>
        </tr>
        <tr>
            <td>Scottsdale Shea Medical Center</td>
            <td>Scottsdale</td>
            <td>AZ</td>
            <td>1471.0</td>
        </tr>
        <tr>
            <td>CHI Health Plainview</td>
            <td>Plainview</td>
            <td>NE</td>
            <td>1473.0</td>
        </tr>
        <tr>
            <td>Greenwich Hospital Association</td>
            <td>Greenwich</td>
            <td>CT</td>
            <td>1474.0</td>
        </tr>
        <tr>
            <td>Oro Valley Hospital</td>
            <td>Oro Valley</td>
            <td>AZ</td>
            <td>1475.0</td>
        </tr>
        <tr>
            <td>Methodist Hospital Stone Oak</td>
            <td>San Antonio</td>
            <td>TX</td>
            <td>1476.0</td>
        </tr>
        <tr>
            <td>Crescent Medical Center Lancaster</td>
            <td>Lancaster</td>
            <td>TX</td>
            <td>1477.0</td>
        </tr>
        <tr>
            <td>Coastal Carolina Hospital</td>
            <td>Hardeeville</td>
            <td>SC</td>
            <td>1478.0</td>
        </tr>
        <tr>
            <td>Huntington Memorial Hospital</td>
            <td>Pasadena</td>
            <td>CA</td>
            <td>1479.0</td>
        </tr>
        <tr>
            <td>Centennial Hills Hospital Medical Center</td>
            <td>Las Vegas</td>
            <td>NV</td>
            <td>1480.0</td>
        </tr>
        <tr>
            <td>Saint Barnabas Medical Center</td>
            <td>Livingston</td>
            <td>NJ</td>
            <td>1481.0</td>
        </tr>
        <tr>
            <td>Porter Regional Hospital</td>
            <td>Valparaiso</td>
            <td>IN</td>
            <td>1482.0</td>
        </tr>
        <tr>
            <td>Central Maine Medical Center</td>
            <td>Lewiston</td>
            <td>ME</td>
            <td>1483.0</td>
        </tr>
        <tr>
            <td>Lake View Memorial Hospital</td>
            <td>Two Harbors</td>
            <td>MN</td>
            <td>1484.0</td>
        </tr>
        <tr>
            <td>Bozeman Health Deaconess Hospital</td>
            <td>Bozeman</td>
            <td>MT</td>
            <td>1485.0</td>
        </tr>
        <tr>
            <td>St. Francis Regional Medical Center</td>
            <td>Shakopee</td>
            <td>MN</td>
            <td>1486.0</td>
        </tr>
        <tr>
            <td>ARH Our Lady of the Way</td>
            <td>Martin</td>
            <td>KY</td>
            <td>1487.0</td>
        </tr>
        <tr>
            <td>Saint Anne&#x27;s Hospital</td>
            <td>Fall River</td>
            <td>MA</td>
            <td>1488.0</td>
        </tr>
        <tr>
            <td>Spencer Municipal Hospital</td>
            <td>Spencer</td>
            <td>IA</td>
            <td>1489.0</td>
        </tr>
        <tr>
            <td>Grand View Hospital</td>
            <td>Sellersville</td>
            <td>PA</td>
            <td>1490.0</td>
        </tr>
        <tr>
            <td>Mary Hitchcock Memorial Hospital</td>
            <td>Lebanon</td>
            <td>NH</td>
            <td>1491.0</td>
        </tr>
        <tr>
            <td>Uf Health Jacksonville</td>
            <td>Jacksonville</td>
            <td>FL</td>
            <td>1492.0</td>
        </tr>
        <tr>
            <td>Centra Lynchburg General Hospital</td>
            <td>Lynchburg</td>
            <td>VA</td>
            <td>1493.0</td>
        </tr>
        <tr>
            <td>Prosser Memorial Hospital</td>
            <td>Prosser</td>
            <td>WA</td>
            <td>1494.0</td>
        </tr>
        <tr>
            <td>University of Vermont Medical Center</td>
            <td>Burlington</td>
            <td>VT</td>
            <td>1495.0</td>
        </tr>
        <tr>
            <td>Maury Regional Hospital</td>
            <td>Columbia</td>
            <td>TN</td>
            <td>1496.0</td>
        </tr>
        <tr>
            <td>Princeton Baptist Medical Center</td>
            <td>Birmingham</td>
            <td>AL</td>
            <td>1497.0</td>
        </tr>
        <tr>
            <td>Ascension Good Samaritan Hospital</td>
            <td>Merrill</td>
            <td>WI</td>
            <td>1498.0</td>
        </tr>
        <tr>
            <td>Winchester Medical Center</td>
            <td>Winchester</td>
            <td>VA</td>
            <td>1499.0</td>
        </tr>
        <tr>
            <td>Longs Peak Hospital</td>
            <td>Longmont</td>
            <td>CO</td>
            <td>1500.0</td>
        </tr>
        <tr>
            <td>Nantucket Cottage Hospital</td>
            <td>Nantucket</td>
            <td>MA</td>
            <td>1501.0</td>
        </tr>
        <tr>
            <td>Billings Clinic Hospital</td>
            <td>Billings</td>
            <td>MT</td>
            <td>1502.0</td>
        </tr>
        <tr>
            <td>Sevier Valley Hospital</td>
            <td>Richfield</td>
            <td>UT</td>
            <td>1503.0</td>
        </tr>
        <tr>
            <td>Mission Hospital McDowell</td>
            <td>Marion</td>
            <td>NC</td>
            <td>1504.0</td>
        </tr>
        <tr>
            <td>Camden General Hospital</td>
            <td>Camden</td>
            <td>TN</td>
            <td>1505.0</td>
        </tr>
        <tr>
            <td>Brookings Health System</td>
            <td>Brookings</td>
            <td>SD</td>
            <td>1506.0</td>
        </tr>
        <tr>
            <td>Novant Health UVAÂ¬â€  Prince William Medical Center</td>
            <td>Manassas</td>
            <td>VA</td>
            <td>1507.0</td>
        </tr>
        <tr>
            <td>Tomah Health</td>
            <td>Tomah</td>
            <td>WI</td>
            <td>1508.0</td>
        </tr>
        <tr>
            <td>Enloe Medical Center</td>
            <td>Chico</td>
            <td>CA</td>
            <td>1509.0</td>
        </tr>
        <tr>
            <td>Frederick Memorial Hospital</td>
            <td>Frederick</td>
            <td>MD</td>
            <td>1510.0</td>
        </tr>
        <tr>
            <td>Sanford Luverne Medical Center</td>
            <td>Luverne</td>
            <td>MN</td>
            <td>1511.0</td>
        </tr>
        <tr>
            <td>Eastern Maine Medical Center</td>
            <td>Bangor</td>
            <td>ME</td>
            <td>1512.0</td>
        </tr>
        <tr>
            <td>Tristar Skyline Medical Center</td>
            <td>Nashville</td>
            <td>TN</td>
            <td>1513.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System-Cannon Falls</td>
            <td>Cannon Falls</td>
            <td>MN</td>
            <td>1514.0</td>
        </tr>
        <tr>
            <td>Moab Regional Hospital</td>
            <td>Moab</td>
            <td>UT</td>
            <td>1515.0</td>
        </tr>
        <tr>
            <td>Carolinas Medical Center</td>
            <td>Charlotte</td>
            <td>NC</td>
            <td>1516.0</td>
        </tr>
        <tr>
            <td>Peace Harbor Medical Center</td>
            <td>Florence</td>
            <td>OR</td>
            <td>1517.0</td>
        </tr>
        <tr>
            <td>SSM Health St. Joseph Hospital-St. Charles</td>
            <td>Saint Charles</td>
            <td>MO</td>
            <td>1518.0</td>
        </tr>
        <tr>
            <td>Carson Valley Medical Center</td>
            <td>Gardnerville</td>
            <td>NV</td>
            <td>1519.0</td>
        </tr>
        <tr>
            <td>Glens Falls Hospital</td>
            <td>Glens Falls</td>
            <td>NY</td>
            <td>1520.0</td>
        </tr>
        <tr>
            <td>Excela Health Westmoreland Hospital</td>
            <td>Greensburg</td>
            <td>PA</td>
            <td>1521.0</td>
        </tr>
        <tr>
            <td>Riverside Regional Medical Center</td>
            <td>Newport News</td>
            <td>VA</td>
            <td>1522.0</td>
        </tr>
        <tr>
            <td>Avera St. Mary&#x27;s Hospital</td>
            <td>Pierre</td>
            <td>SD</td>
            <td>1523.0</td>
        </tr>
        <tr>
            <td>Newport Hospital</td>
            <td>Newport</td>
            <td>RI</td>
            <td>1524.0</td>
        </tr>
        <tr>
            <td>Sanford</td>
            <td>Fargo</td>
            <td>ND</td>
            <td>1525.0</td>
        </tr>
        <tr>
            <td>Queens Hospital Center</td>
            <td>Jamaica</td>
            <td>NY</td>
            <td>1526.0</td>
        </tr>
        <tr>
            <td>Sparrow Clinton Hospital</td>
            <td>Saint Johns</td>
            <td>MI</td>
            <td>1527.0</td>
        </tr>
        <tr>
            <td>Beth Israel Deaconess Medical Center</td>
            <td>Boston</td>
            <td>MA</td>
            <td>1528.0</td>
        </tr>
        <tr>
            <td>Parkview Lagrange Hospital</td>
            <td>Lagrange</td>
            <td>IN</td>
            <td>1529.0</td>
        </tr>
        <tr>
            <td>Cheshire Medical Center</td>
            <td>Keene</td>
            <td>NH</td>
            <td>1530.0</td>
        </tr>
        <tr>
            <td>Community Hospital of Anderson and Madison County</td>
            <td>Anderson</td>
            <td>IN</td>
            <td>1531.0</td>
        </tr>
        <tr>
            <td>Ephraim Mcdowell Regional Medical Center</td>
            <td>Danville</td>
            <td>KY</td>
            <td>1532.0</td>
        </tr>
        <tr>
            <td>Martha&#x27;s Vineyard Hospital</td>
            <td>Oak Bluffs</td>
            <td>MA</td>
            <td>1533.0</td>
        </tr>
        <tr>
            <td>Garrett County Memorial Hospital</td>
            <td>Oakland</td>
            <td>MD</td>
            <td>1534.0</td>
        </tr>
        <tr>
            <td>Presence Saint Francis Hospital</td>
            <td>Evanston</td>
            <td>IL</td>
            <td>1535.0</td>
        </tr>
        <tr>
            <td>St. Tammany Parish Hospital</td>
            <td>Covington</td>
            <td>LA</td>
            <td>1536.0</td>
        </tr>
        <tr>
            <td>Great Plains Health</td>
            <td>North Platte</td>
            <td>NE</td>
            <td>1537.0</td>
        </tr>
        <tr>
            <td>Monmouth Medical Center</td>
            <td>Long Branch</td>
            <td>NJ</td>
            <td>1538.0</td>
        </tr>
        <tr>
            <td>Waupun Memorial Hospital</td>
            <td>Waupun</td>
            <td>WI</td>
            <td>1539.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System-Chippewa Valley</td>
            <td>Bloomer</td>
            <td>WI</td>
            <td>1540.0</td>
        </tr>
        <tr>
            <td>Shelby Baptist Medical Center</td>
            <td>Alabaster</td>
            <td>AL</td>
            <td>1541.0</td>
        </tr>
        <tr>
            <td>Parkridge Medical Center</td>
            <td>Chattanooga</td>
            <td>TN</td>
            <td>1542.0</td>
        </tr>
        <tr>
            <td>Methodist Healthcare - Olive Branch Hospital</td>
            <td>Olive Branch</td>
            <td>MS</td>
            <td>1543.0</td>
        </tr>
        <tr>
            <td>Gundersen Lutheran Medical Center</td>
            <td>La Crosse</td>
            <td>WI</td>
            <td>1544.0</td>
        </tr>
        <tr>
            <td>Golden Plains Community Hospital</td>
            <td>Borger</td>
            <td>TX</td>
            <td>1545.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Magic Valley Rmc</td>
            <td>Twin Falls</td>
            <td>ID</td>
            <td>1546.0</td>
        </tr>
        <tr>
            <td>GHS Greenville Memorial Hospital</td>
            <td>Greenville</td>
            <td>SC</td>
            <td>1547.0</td>
        </tr>
        <tr>
            <td>Nashoba Valley Medical Center</td>
            <td>Ayer</td>
            <td>MA</td>
            <td>1548.0</td>
        </tr>
        <tr>
            <td>Centerpoint Medical Center</td>
            <td>Independence</td>
            <td>MO</td>
            <td>1549.0</td>
        </tr>
        <tr>
            <td>Box Butte General Hospital</td>
            <td>Alliance</td>
            <td>NE</td>
            <td>1550.0</td>
        </tr>
        <tr>
            <td>Marion General Hospital</td>
            <td>Marion</td>
            <td>IN</td>
            <td>1551.0</td>
        </tr>
        <tr>
            <td>Baptist Health Medical Center-Arkadelphia</td>
            <td>Arkadelphia</td>
            <td>AR</td>
            <td>1552.0</td>
        </tr>
        <tr>
            <td>Saint Clare&#x27;s Hospital/ Denville Campus</td>
            <td>Denville</td>
            <td>NJ</td>
            <td>1553.0</td>
        </tr>
        <tr>
            <td>Beverly Hospital Corporation</td>
            <td>Beverly</td>
            <td>MA</td>
            <td>1554.0</td>
        </tr>
        <tr>
            <td>Mary Lanning Healthcare</td>
            <td>Hastings</td>
            <td>NE</td>
            <td>1555.0</td>
        </tr>
        <tr>
            <td>Franciscan Health Indianapolis</td>
            <td>Indianapolis</td>
            <td>IN</td>
            <td>1556.0</td>
        </tr>
        <tr>
            <td>Southern Ohio Medical Center</td>
            <td>Portsmouth</td>
            <td>OH</td>
            <td>1557.0</td>
        </tr>
        <tr>
            <td>University Hospital</td>
            <td>Augusta</td>
            <td>GA</td>
            <td>1558.0</td>
        </tr>
        <tr>
            <td>RumfordÂ¬â€ Hospital</td>
            <td>Rumford</td>
            <td>ME</td>
            <td>1559.0</td>
        </tr>
        <tr>
            <td>Camden Clark Medical Center</td>
            <td>Parkersburg</td>
            <td>WV</td>
            <td>1560.0</td>
        </tr>
        <tr>
            <td>St. Vincents Blount</td>
            <td>Oneonta</td>
            <td>AL</td>
            <td>1561.0</td>
        </tr>
        <tr>
            <td>Central Vermont Medical Center</td>
            <td>Barre</td>
            <td>VT</td>
            <td>1562.0</td>
        </tr>
        <tr>
            <td>Emory University Hospital</td>
            <td>Atlanta</td>
            <td>GA</td>
            <td>1563.0</td>
        </tr>
        <tr>
            <td>Lima Memorial Health System</td>
            <td>Lima</td>
            <td>OH</td>
            <td>1564.0</td>
        </tr>
        <tr>
            <td>Baystate Franklin Medical Center</td>
            <td>Greenfield</td>
            <td>MA</td>
            <td>1565.0</td>
        </tr>
        <tr>
            <td>Baylor Scott &amp; White Medical Center Hillcrest</td>
            <td>Waco</td>
            <td>TX</td>
            <td>1566.0</td>
        </tr>
        <tr>
            <td>Essentia Health St. Joseph&#x27;s Medical Center</td>
            <td>Brainerd</td>
            <td>MN</td>
            <td>1567.0</td>
        </tr>
        <tr>
            <td>Akron General Medical Center</td>
            <td>Akron</td>
            <td>OH</td>
            <td>1568.0</td>
        </tr>
        <tr>
            <td>Altru Hospital</td>
            <td>Grand Forks</td>
            <td>ND</td>
            <td>1569.0</td>
        </tr>
        <tr>
            <td>Shannon Medical Center</td>
            <td>San Angelo</td>
            <td>TX</td>
            <td>1570.0</td>
        </tr>
        <tr>
            <td>Chinese Hospital</td>
            <td>San Francisco</td>
            <td>CA</td>
            <td>1571.0</td>
        </tr>
        <tr>
            <td>Ottawa Regional Hospital &amp; Healthcare Center</td>
            <td>Ottawa</td>
            <td>IL</td>
            <td>1572.0</td>
        </tr>
        <tr>
            <td>Mercy Health-Lorain Hospital</td>
            <td>Lorain</td>
            <td>OH</td>
            <td>1573.0</td>
        </tr>
        <tr>
            <td>Ochsner Medical Center</td>
            <td>New Orleans</td>
            <td>LA</td>
            <td>1574.0</td>
        </tr>
        <tr>
            <td>Medstar Georgetown University Hospital</td>
            <td>Washington</td>
            <td>DC</td>
            <td>1575.0</td>
        </tr>
        <tr>
            <td>Northern Light Mercy Hospital</td>
            <td>Portland</td>
            <td>ME</td>
            <td>1576.0</td>
        </tr>
        <tr>
            <td>Henry Ford Hospital</td>
            <td>Detroit</td>
            <td>MI</td>
            <td>1578.0</td>
        </tr>
        <tr>
            <td>St. Joseph&#x27;s Hospital - Savannah</td>
            <td>Savannah</td>
            <td>GA</td>
            <td>1579.0</td>
        </tr>
        <tr>
            <td>Southern NH Medical Center</td>
            <td>Nashua</td>
            <td>NH</td>
            <td>1580.0</td>
        </tr>
        <tr>
            <td>UPMC Somerset</td>
            <td>Somerset</td>
            <td>PA</td>
            <td>1581.0</td>
        </tr>
        <tr>
            <td>Mercy San Juan Medical Center</td>
            <td>Carmichael</td>
            <td>CA</td>
            <td>1582.0</td>
        </tr>
        <tr>
            <td>EvergreenHealth Monroe</td>
            <td>Monroe</td>
            <td>WA</td>
            <td>1583.0</td>
        </tr>
        <tr>
            <td>Inspira Medical Center Vineland</td>
            <td>Vineland</td>
            <td>NJ</td>
            <td>1584.0</td>
        </tr>
        <tr>
            <td>University of South Alabama Medical Center</td>
            <td>Mobile</td>
            <td>AL</td>
            <td>1585.0</td>
        </tr>
        <tr>
            <td>Aspirus Wausau Hospital</td>
            <td>Wausau</td>
            <td>WI</td>
            <td>1586.0</td>
        </tr>
        <tr>
            <td>The Monroe Clinic</td>
            <td>Monroe</td>
            <td>WI</td>
            <td>1587.0</td>
        </tr>
        <tr>
            <td>Presbyterian Hospital</td>
            <td>Albuquerque</td>
            <td>NM</td>
            <td>1588.0</td>
        </tr>
        <tr>
            <td>Heart of the Rockies Regional Medical Center</td>
            <td>Salida</td>
            <td>CO</td>
            <td>1589.0</td>
        </tr>
        <tr>
            <td>Ellis Hospital</td>
            <td>Schenectady</td>
            <td>NY</td>
            <td>1590.0</td>
        </tr>
        <tr>
            <td>Moberly Regional Medical Center</td>
            <td>Moberly</td>
            <td>MO</td>
            <td>1591.0</td>
        </tr>
        <tr>
            <td>Atrium Medical Center</td>
            <td>Franklin</td>
            <td>OH</td>
            <td>1592.0</td>
        </tr>
        <tr>
            <td>Tri-State Memorial Hospital</td>
            <td>Clarkston</td>
            <td>WA</td>
            <td>1593.0</td>
        </tr>
        <tr>
            <td>Wentworth-Douglass Hospital</td>
            <td>Dover</td>
            <td>NH</td>
            <td>1594.0</td>
        </tr>
        <tr>
            <td>Seton Edgar B. Davis Hospital</td>
            <td>Luling</td>
            <td>TX</td>
            <td>1595.0</td>
        </tr>
        <tr>
            <td>Palisades Medical Center</td>
            <td>North Bergen</td>
            <td>NJ</td>
            <td>1596.0</td>
        </tr>
        <tr>
            <td>The Washington Hospital</td>
            <td>Washington</td>
            <td>PA</td>
            <td>1597.0</td>
        </tr>
        <tr>
            <td>Sparrow Ionia Hospital</td>
            <td>Ionia</td>
            <td>MI</td>
            <td>1598.0</td>
        </tr>
        <tr>
            <td>Westerly Hospital</td>
            <td>Westerly</td>
            <td>RI</td>
            <td>1599.0</td>
        </tr>
        <tr>
            <td>Valley Baptist Medical Center- Brownsville</td>
            <td>Brownsville</td>
            <td>TX</td>
            <td>1600.0</td>
        </tr>
        <tr>
            <td>New York-Presbyterian/Hudson Valley Hospital</td>
            <td>Cortlandt Manor</td>
            <td>NY</td>
            <td>1601.0</td>
        </tr>
        <tr>
            <td>Grinnell Regional Medical Center</td>
            <td>Grinnell</td>
            <td>IA</td>
            <td>1602.0</td>
        </tr>
        <tr>
            <td>UT Health East Texas Quitman Hospital</td>
            <td>Quitman</td>
            <td>TX</td>
            <td>1603.0</td>
        </tr>
        <tr>
            <td>Harris Health System</td>
            <td>Houston</td>
            <td>TX</td>
            <td>1604.0</td>
        </tr>
        <tr>
            <td>Catholic Medical Center</td>
            <td>Manchester</td>
            <td>NH</td>
            <td>1605.0</td>
        </tr>
        <tr>
            <td>Henry Ford Allegiance Health</td>
            <td>Jackson</td>
            <td>MI</td>
            <td>1606.0</td>
        </tr>
        <tr>
            <td>University of Washington Medical Center</td>
            <td>Seattle</td>
            <td>WA</td>
            <td>1607.0</td>
        </tr>
        <tr>
            <td>Alhambra Hospital Medical Center</td>
            <td>Alhambra</td>
            <td>CA</td>
            <td>1608.0</td>
        </tr>
        <tr>
            <td>Northwestern Lake Forest Hospital</td>
            <td>Lake Forest</td>
            <td>IL</td>
            <td>1609.0</td>
        </tr>
        <tr>
            <td>OSF Saint Paul Medical Center</td>
            <td>Mendota</td>
            <td>IL</td>
            <td>1610.0</td>
        </tr>
        <tr>
            <td>Banner - University Medical Center Tucson Campus</td>
            <td>Tucson</td>
            <td>AZ</td>
            <td>1611.0</td>
        </tr>
        <tr>
            <td>Spectrum Health - Butterworth Campus</td>
            <td>Grand Rapids</td>
            <td>MI</td>
            <td>1612.0</td>
        </tr>
        <tr>
            <td>Whidbeyhealth Medical Center</td>
            <td>Coupeville</td>
            <td>WA</td>
            <td>1613.0</td>
        </tr>
        <tr>
            <td>Ojai Valley Community Hospital</td>
            <td>Ojai</td>
            <td>CA</td>
            <td>1614.0</td>
        </tr>
        <tr>
            <td>Barnes Jewish Hospital</td>
            <td>Saint Louis</td>
            <td>MO</td>
            <td>1615.0</td>
        </tr>
        <tr>
            <td>Centracare Health System - Long Prairie</td>
            <td>Long Prairie</td>
            <td>MN</td>
            <td>1616.0</td>
        </tr>
        <tr>
            <td>East Morgan County Hospital</td>
            <td>Brush</td>
            <td>CO</td>
            <td>1617.0</td>
        </tr>
        <tr>
            <td>Seton Medical Center Harker Heights</td>
            <td>Harker Heights</td>
            <td>TX</td>
            <td>1618.0</td>
        </tr>
        <tr>
            <td>Adventist Health Simi Valley</td>
            <td>Simi Valley</td>
            <td>CA</td>
            <td>1619.0</td>
        </tr>
        <tr>
            <td>Minidoka Memorial Hospital</td>
            <td>Rupert</td>
            <td>ID</td>
            <td>1620.0</td>
        </tr>
        <tr>
            <td>Norwalk Hospital Association</td>
            <td>Norwalk</td>
            <td>CT</td>
            <td>1621.0</td>
        </tr>
        <tr>
            <td>Woodland Memorial Hospital</td>
            <td>Woodland</td>
            <td>CA</td>
            <td>1622.0</td>
        </tr>
        <tr>
            <td>Norwegian-American Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>1623.0</td>
        </tr>
        <tr>
            <td>UPMC Presbyterian Shadyside</td>
            <td>Pittsburgh</td>
            <td>PA</td>
            <td>1624.0</td>
        </tr>
        <tr>
            <td>Texas Health Harris Methodist Hospital Alliance</td>
            <td>Fort Worth</td>
            <td>TX</td>
            <td>1625.0</td>
        </tr>
        <tr>
            <td>North Carolina Baptist Hospital</td>
            <td>Winston-Salem</td>
            <td>NC</td>
            <td>1626.0</td>
        </tr>
        <tr>
            <td>Aurora Baycare Medical Center</td>
            <td>Green Bay</td>
            <td>WI</td>
            <td>1627.0</td>
        </tr>
        <tr>
            <td>Charlotte Hungerford Hospital</td>
            <td>Torrington</td>
            <td>CT</td>
            <td>1628.0</td>
        </tr>
        <tr>
            <td>Marshfield Medical Center</td>
            <td>Marshfield</td>
            <td>WI</td>
            <td>1629.0</td>
        </tr>
        <tr>
            <td>Lehigh Valley Hospital - Pocono</td>
            <td>East Stroudsburg</td>
            <td>PA</td>
            <td>1630.0</td>
        </tr>
        <tr>
            <td>Saint Francis Medical Center</td>
            <td>Peoria</td>
            <td>IL</td>
            <td>1631.0</td>
        </tr>
        <tr>
            <td>Riverton Hospital</td>
            <td>Riverton</td>
            <td>UT</td>
            <td>1632.0</td>
        </tr>
        <tr>
            <td>St. Margarets Hospital</td>
            <td>Spring Valley</td>
            <td>IL</td>
            <td>1633.0</td>
        </tr>
        <tr>
            <td>Orange Regional Medical Center</td>
            <td>Middletown</td>
            <td>NY</td>
            <td>1634.0</td>
        </tr>
        <tr>
            <td>Lewisgale Medical Center</td>
            <td>Salem</td>
            <td>VA</td>
            <td>1635.0</td>
        </tr>
        <tr>
            <td>Aspirus Medford Hospital &amp; Clinics</td>
            <td>Medford</td>
            <td>WI</td>
            <td>1636.0</td>
        </tr>
        <tr>
            <td>UF Health Shands Hospital</td>
            <td>Gainesville</td>
            <td>FL</td>
            <td>1637.0</td>
        </tr>
        <tr>
            <td>University of Iowa Hospital &amp; Clinics</td>
            <td>Iowa City</td>
            <td>IA</td>
            <td>1638.0</td>
        </tr>
        <tr>
            <td>Sidney Health Center</td>
            <td>Sidney</td>
            <td>MT</td>
            <td>1639.0</td>
        </tr>
        <tr>
            <td>Indiana University Health Ball Memorial Hospital</td>
            <td>Muncie</td>
            <td>IN</td>
            <td>1640.0</td>
        </tr>
        <tr>
            <td>Trinity Regional Medical Center</td>
            <td>Fort Dodge</td>
            <td>IA</td>
            <td>1641.0</td>
        </tr>
        <tr>
            <td>Windham Comm Mem Hosp &amp; Hatch Hosp</td>
            <td>Willimantic</td>
            <td>CT</td>
            <td>1642.0</td>
        </tr>
        <tr>
            <td>Baptist Medical Center - Nassau</td>
            <td>Fernandina Beach</td>
            <td>FL</td>
            <td>1643.0</td>
        </tr>
        <tr>
            <td>Mercy Health System</td>
            <td>Janesville</td>
            <td>WI</td>
            <td>1644.0</td>
        </tr>
        <tr>
            <td>Methodist Charlton Medical Center</td>
            <td>Dallas</td>
            <td>TX</td>
            <td>1645.0</td>
        </tr>
        <tr>
            <td>Genesis Hospital</td>
            <td>Zanesville</td>
            <td>OH</td>
            <td>1646.0</td>
        </tr>
        <tr>
            <td>Hartford Hospital</td>
            <td>Hartford</td>
            <td>CT</td>
            <td>1647.0</td>
        </tr>
        <tr>
            <td>La Palma Intercommunity Hospital</td>
            <td>La Palma</td>
            <td>CA</td>
            <td>1648.0</td>
        </tr>
        <tr>
            <td>Adventist Glenoaks</td>
            <td>Glendale Heights</td>
            <td>IL</td>
            <td>1649.0</td>
        </tr>
        <tr>
            <td>Citizens Memorial Hospital</td>
            <td>Bolivar</td>
            <td>MO</td>
            <td>1650.0</td>
        </tr>
        <tr>
            <td>Providence St. Peter Hospital</td>
            <td>Olympia</td>
            <td>WA</td>
            <td>1651.0</td>
        </tr>
        <tr>
            <td>UAB Hospital</td>
            <td>Birmingham</td>
            <td>AL</td>
            <td>1652.0</td>
        </tr>
        <tr>
            <td>Bigfork Valley Hospital</td>
            <td>Bigfork</td>
            <td>MN</td>
            <td>1653.0</td>
        </tr>
        <tr>
            <td>Brooklyn Hospital Center - Downtown Campus</td>
            <td>Brooklyn</td>
            <td>NY</td>
            <td>1654.0</td>
        </tr>
        <tr>
            <td>UPMC East</td>
            <td>Monroeville</td>
            <td>PA</td>
            <td>1655.0</td>
        </tr>
        <tr>
            <td>Novant Health Presbyterian Medical Center</td>
            <td>Charlotte</td>
            <td>NC</td>
            <td>1656.0</td>
        </tr>
        <tr>
            <td>Starke Hospital</td>
            <td>Knox</td>
            <td>IN</td>
            <td>1657.0</td>
        </tr>
        <tr>
            <td>Bay Area Hospital</td>
            <td>Coos Bay</td>
            <td>OR</td>
            <td>1658.0</td>
        </tr>
        <tr>
            <td>Stephens Memorial Hospital</td>
            <td>Norway</td>
            <td>ME</td>
            <td>1661.0</td>
        </tr>
        <tr>
            <td>Hillcrest Medical Center</td>
            <td>Tulsa</td>
            <td>OK</td>
            <td>1662.0</td>
        </tr>
        <tr>
            <td>Methodist Hospitals</td>
            <td>Gary</td>
            <td>IN</td>
            <td>1663.0</td>
        </tr>
        <tr>
            <td>St. Joseph Hospital</td>
            <td>Fort Wayne</td>
            <td>IN</td>
            <td>1664.0</td>
        </tr>
        <tr>
            <td>Ochsner Medical Center-Kenner</td>
            <td>Kenner</td>
            <td>LA</td>
            <td>1665.0</td>
        </tr>
        <tr>
            <td>Catawba Valley Medical Center</td>
            <td>Hickory</td>
            <td>NC</td>
            <td>1666.0</td>
        </tr>
        <tr>
            <td>Franklin Woods Community Hospital</td>
            <td>Johnson City</td>
            <td>TN</td>
            <td>1667.0</td>
        </tr>
        <tr>
            <td>University of North Carolina Hospital</td>
            <td>Chapel Hill</td>
            <td>NC</td>
            <td>1668.0</td>
        </tr>
        <tr>
            <td>Anne Arundel Medical Center</td>
            <td>Annapolis</td>
            <td>MD</td>
            <td>1669.0</td>
        </tr>
        <tr>
            <td>Bon Secours Depaul Medical Center</td>
            <td>Norfolk</td>
            <td>VA</td>
            <td>1670.0</td>
        </tr>
        <tr>
            <td>St. Vincent Kokomo</td>
            <td>Kokomo</td>
            <td>IN</td>
            <td>1671.0</td>
        </tr>
        <tr>
            <td>Lexington Memorial Hospital</td>
            <td>Lexington</td>
            <td>NC</td>
            <td>1672.0</td>
        </tr>
        <tr>
            <td>Saint Anthony Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>1673.0</td>
        </tr>
        <tr>
            <td>University of Maryland Harford Memorial Hospital</td>
            <td>Havre De Grace</td>
            <td>MD</td>
            <td>1674.0</td>
        </tr>
        <tr>
            <td>Banner Baywood Medical Center</td>
            <td>Mesa</td>
            <td>AZ</td>
            <td>1675.0</td>
        </tr>
        <tr>
            <td>Long Island Jewish Medical Center</td>
            <td>New Hyde Park</td>
            <td>NY</td>
            <td>1676.0</td>
        </tr>
        <tr>
            <td>Regional Medical Center Bayonet Point</td>
            <td>Hudson</td>
            <td>FL</td>
            <td>1677.0</td>
        </tr>
        <tr>
            <td>Mckenzie-Willamette Medical Center</td>
            <td>Springfield</td>
            <td>OR</td>
            <td>1678.0</td>
        </tr>
        <tr>
            <td>Grand Itasca Clinic and Hospital</td>
            <td>Grand Rapids</td>
            <td>MN</td>
            <td>1679.0</td>
        </tr>
        <tr>
            <td>Metrowest Medical Center</td>
            <td>Framingham</td>
            <td>MA</td>
            <td>1680.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Lebanon</td>
            <td>Lebanon</td>
            <td>MO</td>
            <td>1681.0</td>
        </tr>
        <tr>
            <td>Johnston Health</td>
            <td>Smithfield</td>
            <td>NC</td>
            <td>1682.0</td>
        </tr>
        <tr>
            <td>UH Cleveland Medical Center</td>
            <td>Cleveland</td>
            <td>OH</td>
            <td>1683.0</td>
        </tr>
        <tr>
            <td>Maine General Medical Center</td>
            <td>Augusta</td>
            <td>ME</td>
            <td>1684.0</td>
        </tr>
        <tr>
            <td>Novant Health Forsyth Medical Center</td>
            <td>Winston-Salem</td>
            <td>NC</td>
            <td>1685.0</td>
        </tr>
        <tr>
            <td>St. Vincent&#x27;s East</td>
            <td>Birmingham</td>
            <td>AL</td>
            <td>1686.0</td>
        </tr>
        <tr>
            <td>Adventist Health Hanford</td>
            <td>Hanford</td>
            <td>CA</td>
            <td>1687.0</td>
        </tr>
        <tr>
            <td>Midstate Medical Center</td>
            <td>Meriden</td>
            <td>CT</td>
            <td>1688.0</td>
        </tr>
        <tr>
            <td>Adventist Healthcare Shady Grove Medical Center</td>
            <td>Rockville</td>
            <td>MD</td>
            <td>1689.0</td>
        </tr>
        <tr>
            <td>St. Elizabeth&#x27;s Medical Center</td>
            <td>Brighton</td>
            <td>MA</td>
            <td>1690.0</td>
        </tr>
        <tr>
            <td>Reynolds Memorial Hospital</td>
            <td>Glen Dale</td>
            <td>WV</td>
            <td>1691.0</td>
        </tr>
        <tr>
            <td>San Dimas Community Hospital</td>
            <td>San Dimas</td>
            <td>CA</td>
            <td>1692.0</td>
        </tr>
        <tr>
            <td>Tri-City Medical Center</td>
            <td>Oceanside</td>
            <td>CA</td>
            <td>1693.0</td>
        </tr>
        <tr>
            <td>Blount Memorial Hospital</td>
            <td>Maryville</td>
            <td>TN</td>
            <td>1694.0</td>
        </tr>
        <tr>
            <td>Renown South Meadows Medical Center</td>
            <td>Reno</td>
            <td>NV</td>
            <td>1695.0</td>
        </tr>
        <tr>
            <td>Grossmont Hospital</td>
            <td>La Mesa</td>
            <td>CA</td>
            <td>1696.0</td>
        </tr>
        <tr>
            <td>Sumner Regional Medical Center</td>
            <td>Gallatin</td>
            <td>TN</td>
            <td>1697.0</td>
        </tr>
        <tr>
            <td>St. Elizabeth Florence</td>
            <td>Florence</td>
            <td>KY</td>
            <td>1698.0</td>
        </tr>
        <tr>
            <td>Regional Health Rapid City Hospital</td>
            <td>Rapid City</td>
            <td>SD</td>
            <td>1699.0</td>
        </tr>
        <tr>
            <td>Beaumont Hospital - Dearborn</td>
            <td>Dearborn</td>
            <td>MI</td>
            <td>1700.0</td>
        </tr>
        <tr>
            <td>Athol Memorial Hospital</td>
            <td>Athol</td>
            <td>MA</td>
            <td>1701.0</td>
        </tr>
        <tr>
            <td>Gundersen Boscobel Area Hospital and Clinics</td>
            <td>Boscobel</td>
            <td>WI</td>
            <td>1702.0</td>
        </tr>
        <tr>
            <td>MacNealÂ¬â€  Hospital</td>
            <td>Berwyn</td>
            <td>IL</td>
            <td>1703.0</td>
        </tr>
        <tr>
            <td>Trinity Muscatine</td>
            <td>Muscatine</td>
            <td>IA</td>
            <td>1704.0</td>
        </tr>
        <tr>
            <td>CHI-St. Vincent Infirmary</td>
            <td>Little Rock</td>
            <td>AR</td>
            <td>1705.0</td>
        </tr>
        <tr>
            <td>Caromont Regional Medical Center</td>
            <td>Gastonia</td>
            <td>NC</td>
            <td>1706.0</td>
        </tr>
        <tr>
            <td>Piedmont Medical Center</td>
            <td>Rock Hill</td>
            <td>SC</td>
            <td>1707.0</td>
        </tr>
        <tr>
            <td>Redington Fairview General Hospital</td>
            <td>Skowhegan</td>
            <td>ME</td>
            <td>1708.0</td>
        </tr>
        <tr>
            <td>Providence Health Center</td>
            <td>Waco</td>
            <td>TX</td>
            <td>1709.0</td>
        </tr>
        <tr>
            <td>Mercy Medical Center</td>
            <td>Springfield</td>
            <td>MA</td>
            <td>1710.0</td>
        </tr>
        <tr>
            <td>Community Howard Regional Health</td>
            <td>Kokomo</td>
            <td>IN</td>
            <td>1711.0</td>
        </tr>
        <tr>
            <td>Thedacare Regional Medical Center - Appleton</td>
            <td>Appleton</td>
            <td>WI</td>
            <td>1712.0</td>
        </tr>
        <tr>
            <td>Adventist Health Clearlake</td>
            <td>Clearlake</td>
            <td>CA</td>
            <td>1713.0</td>
        </tr>
        <tr>
            <td>Hollywood Presbyterian Medical Center</td>
            <td>Los Angeles</td>
            <td>CA</td>
            <td>1714.0</td>
        </tr>
        <tr>
            <td>Southside Regional Medical Center</td>
            <td>Petersburg</td>
            <td>VA</td>
            <td>1715.0</td>
        </tr>
        <tr>
            <td>Advocate Illinois Masonic Medical Center</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>1716.0</td>
        </tr>
        <tr>
            <td>University of Maryland Charles RegionalÂ¬â€  Medical Center</td>
            <td>La Plata</td>
            <td>MD</td>
            <td>1717.0</td>
        </tr>
        <tr>
            <td>Mercy Medical Center Of Mt Shasta</td>
            <td>Mount Shasta</td>
            <td>CA</td>
            <td>1718.0</td>
        </tr>
        <tr>
            <td>Rhode Island Hospital</td>
            <td>Providence</td>
            <td>RI</td>
            <td>1719.0</td>
        </tr>
        <tr>
            <td>Twin Cities Hospital</td>
            <td>Niceville</td>
            <td>FL</td>
            <td>1720.0</td>
        </tr>
        <tr>
            <td>Loyola University Medical Center</td>
            <td>Maywood</td>
            <td>IL</td>
            <td>1721.0</td>
        </tr>
        <tr>
            <td>Doylestown Hospital</td>
            <td>Doylestown</td>
            <td>PA</td>
            <td>1722.0</td>
        </tr>
        <tr>
            <td>Clara Maass Medical Center</td>
            <td>Belleville</td>
            <td>NJ</td>
            <td>1723.0</td>
        </tr>
        <tr>
            <td>Johnson City Medical Center</td>
            <td>Johnson City</td>
            <td>TN</td>
            <td>1724.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Jefferson</td>
            <td>Festus</td>
            <td>MO</td>
            <td>1725.0</td>
        </tr>
        <tr>
            <td>Vassar Brothers Medical Center</td>
            <td>Poughkeepsie</td>
            <td>NY</td>
            <td>1726.0</td>
        </tr>
        <tr>
            <td>Northeast Georgia Medical Center</td>
            <td>Gainesville</td>
            <td>GA</td>
            <td>1727.0</td>
        </tr>
        <tr>
            <td>Blue Ridge Regional Hospital</td>
            <td>Spruce Pine</td>
            <td>NC</td>
            <td>1728.0</td>
        </tr>
        <tr>
            <td>St. Charles Hospital</td>
            <td>Port Jefferson</td>
            <td>NY</td>
            <td>1729.0</td>
        </tr>
        <tr>
            <td>North Shore University Hospital</td>
            <td>Manhasset</td>
            <td>NY</td>
            <td>1730.0</td>
        </tr>
        <tr>
            <td>Ascension Ne Wisconsin - St. Elizabeth Campus</td>
            <td>Appleton</td>
            <td>WI</td>
            <td>1731.0</td>
        </tr>
        <tr>
            <td>Riverwood Healthcare Center</td>
            <td>Aitkin</td>
            <td>MN</td>
            <td>1732.0</td>
        </tr>
        <tr>
            <td>St. Claire Regional Medical Center</td>
            <td>Morehead</td>
            <td>KY</td>
            <td>1733.0</td>
        </tr>
        <tr>
            <td>HCA Houston Healthcare Conroe</td>
            <td>Conroe</td>
            <td>TX</td>
            <td>1734.0</td>
        </tr>
        <tr>
            <td>Hialeah Hospital</td>
            <td>Hialeah</td>
            <td>FL</td>
            <td>1735.0</td>
        </tr>
        <tr>
            <td>Wilcox Memorial Hospital</td>
            <td>Lihue</td>
            <td>HI</td>
            <td>1736.0</td>
        </tr>
        <tr>
            <td>Sierra Nevada Memorial Hospital</td>
            <td>Grass Valley</td>
            <td>CA</td>
            <td>1737.0</td>
        </tr>
        <tr>
            <td>Elkhart General Hospital</td>
            <td>Elkhart</td>
            <td>IN</td>
            <td>1738.0</td>
        </tr>
        <tr>
            <td>Beloit Memorial Hospital</td>
            <td>Beloit</td>
            <td>WI</td>
            <td>1739.0</td>
        </tr>
        <tr>
            <td>Passavant Area Hospital</td>
            <td>Jacksonville</td>
            <td>IL</td>
            <td>1740.0</td>
        </tr>
        <tr>
            <td>Stafford Hospital</td>
            <td>Stafford</td>
            <td>VA</td>
            <td>1741.0</td>
        </tr>
        <tr>
            <td>Medical Center of Trinity</td>
            <td>Trinity</td>
            <td>FL</td>
            <td>1742.0</td>
        </tr>
        <tr>
            <td>Berlin Memorial Hospital</td>
            <td>Berlin</td>
            <td>WI</td>
            <td>1743.0</td>
        </tr>
        <tr>
            <td>MelroseWakefield Healthcare</td>
            <td>Melrose</td>
            <td>MA</td>
            <td>1744.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital of South Bend</td>
            <td>South Bend</td>
            <td>IN</td>
            <td>1745.0</td>
        </tr>
        <tr>
            <td>Ascension St. John Hospital</td>
            <td>Detroit</td>
            <td>MI</td>
            <td>1746.0</td>
        </tr>
        <tr>
            <td>Cape Cod Hospital</td>
            <td>Hyannis</td>
            <td>MA</td>
            <td>1747.0</td>
        </tr>
        <tr>
            <td>Robert Wood Johnson University Hospital Somerset</td>
            <td>Somerville</td>
            <td>NJ</td>
            <td>1748.0</td>
        </tr>
        <tr>
            <td>Singing River Health System</td>
            <td>Pascagoula</td>
            <td>MS</td>
            <td>1749.0</td>
        </tr>
        <tr>
            <td>Aria Health</td>
            <td>Philadelphia</td>
            <td>PA</td>
            <td>1750.0</td>
        </tr>
        <tr>
            <td>Wellstar West Georgia Medical Center</td>
            <td>Lagrange</td>
            <td>GA</td>
            <td>1751.0</td>
        </tr>
        <tr>
            <td>Ochsner Medical Center-Hancock</td>
            <td>Bay Saint Louis</td>
            <td>MS</td>
            <td>1752.0</td>
        </tr>
        <tr>
            <td>Texas Health Harris Methodist Hospital Cleburne</td>
            <td>Cleburne</td>
            <td>TX</td>
            <td>1753.0</td>
        </tr>
        <tr>
            <td>North Shore Medical Center</td>
            <td>Miami</td>
            <td>FL</td>
            <td>1754.0</td>
        </tr>
        <tr>
            <td>Jefferson Hospital</td>
            <td>Louisville</td>
            <td>GA</td>
            <td>1755.0</td>
        </tr>
        <tr>
            <td>Medical City Denton</td>
            <td>Denton</td>
            <td>TX</td>
            <td>1756.0</td>
        </tr>
        <tr>
            <td>Lower Keys Medical Center</td>
            <td>Key West</td>
            <td>FL</td>
            <td>1757.0</td>
        </tr>
        <tr>
            <td>Mid Coast Hospital</td>
            <td>Brunswick</td>
            <td>ME</td>
            <td>1758.0</td>
        </tr>
        <tr>
            <td>Capital Regional Medical Center</td>
            <td>Tallahassee</td>
            <td>FL</td>
            <td>1759.0</td>
        </tr>
        <tr>
            <td>Baylor Scott &amp; White Medical Center- College Stati</td>
            <td>College Station</td>
            <td>TX</td>
            <td>1760.0</td>
        </tr>
        <tr>
            <td>Richland Hospital</td>
            <td>Richland Center</td>
            <td>WI</td>
            <td>1761.0</td>
        </tr>
        <tr>
            <td>Tulane Medical Center</td>
            <td>New Orleans</td>
            <td>LA</td>
            <td>1762.0</td>
        </tr>
        <tr>
            <td>Danbury Hospital</td>
            <td>Danbury</td>
            <td>CT</td>
            <td>1763.0</td>
        </tr>
        <tr>
            <td>Parkview Whitley Hospital</td>
            <td>Columbia City</td>
            <td>IN</td>
            <td>1764.0</td>
        </tr>
        <tr>
            <td>Brookdale Hospital Medical Center</td>
            <td>Brooklyn</td>
            <td>NY</td>
            <td>1765.0</td>
        </tr>
        <tr>
            <td>St. Vincent&#x27;s Chilton</td>
            <td>Clanton</td>
            <td>AL</td>
            <td>1766.0</td>
        </tr>
        <tr>
            <td>Our Lady of Lourdes Medical Center</td>
            <td>Camden</td>
            <td>NJ</td>
            <td>1767.0</td>
        </tr>
        <tr>
            <td>Medstar Good Samaritan Hospital</td>
            <td>Baltimore</td>
            <td>MD</td>
            <td>1768.0</td>
        </tr>
        <tr>
            <td>Clark Memorial Hospital</td>
            <td>Jeffersonville</td>
            <td>IN</td>
            <td>1769.0</td>
        </tr>
        <tr>
            <td>Mercy Health Lakeshore Campus</td>
            <td>Shelby</td>
            <td>MI</td>
            <td>1770.0</td>
        </tr>
        <tr>
            <td>Hardin Memorial Hospital</td>
            <td>Elizabethtown</td>
            <td>KY</td>
            <td>1771.0</td>
        </tr>
        <tr>
            <td>Hayes Green Beach Memorial Hospital</td>
            <td>Charlotte</td>
            <td>MI</td>
            <td>1772.0</td>
        </tr>
        <tr>
            <td>Pagosa Springs Medical Center</td>
            <td>Pagosa Springs</td>
            <td>CO</td>
            <td>1773.0</td>
        </tr>
        <tr>
            <td>Methodist Jennie Edmundson</td>
            <td>Council Bluffs</td>
            <td>IA</td>
            <td>1774.0</td>
        </tr>
        <tr>
            <td>Miami Valley Hospital</td>
            <td>Dayton</td>
            <td>OH</td>
            <td>1775.0</td>
        </tr>
        <tr>
            <td>McLaren Macomb</td>
            <td>Mount Clemens</td>
            <td>MI</td>
            <td>1776.0</td>
        </tr>
        <tr>
            <td>Lake Wales Medical Center</td>
            <td>Lake Wales</td>
            <td>FL</td>
            <td>1777.0</td>
        </tr>
        <tr>
            <td>Sanpete Valley Hospital</td>
            <td>Mount Pleasant</td>
            <td>UT</td>
            <td>1778.0</td>
        </tr>
        <tr>
            <td>Sidney Regional Medical Center</td>
            <td>Sidney</td>
            <td>NE</td>
            <td>1779.0</td>
        </tr>
        <tr>
            <td>Touro Infirmary</td>
            <td>New Orleans</td>
            <td>LA</td>
            <td>1780.0</td>
        </tr>
        <tr>
            <td>Hopedale Hospital</td>
            <td>Hopedale</td>
            <td>IL</td>
            <td>1781.0</td>
        </tr>
        <tr>
            <td>University of Texas Medical Branch</td>
            <td>Galveston</td>
            <td>TX</td>
            <td>1782.0</td>
        </tr>
        <tr>
            <td>Golden Valley Memorial Hospital</td>
            <td>Clinton</td>
            <td>MO</td>
            <td>1783.0</td>
        </tr>
        <tr>
            <td>PIH Health Hospital-Whittier</td>
            <td>Whittier</td>
            <td>CA</td>
            <td>1784.0</td>
        </tr>
        <tr>
            <td>Albany Medical Center Hospital</td>
            <td>Albany</td>
            <td>NY</td>
            <td>1785.0</td>
        </tr>
        <tr>
            <td>Parkwest Medical Center</td>
            <td>Knoxville</td>
            <td>TN</td>
            <td>1786.0</td>
        </tr>
        <tr>
            <td>Methodist Healthcare Memphis Hospitals</td>
            <td>Memphis</td>
            <td>TN</td>
            <td>1787.0</td>
        </tr>
        <tr>
            <td>Aventura Hospital and Medical Center</td>
            <td>Aventura</td>
            <td>FL</td>
            <td>1788.0</td>
        </tr>
        <tr>
            <td>Northside Hospital</td>
            <td>Saint Petersburg</td>
            <td>FL</td>
            <td>1789.0</td>
        </tr>
        <tr>
            <td>Sibley Memorial Hospital</td>
            <td>Washington</td>
            <td>DC</td>
            <td>1790.0</td>
        </tr>
        <tr>
            <td>Santiam Hospital</td>
            <td>Stayton</td>
            <td>OR</td>
            <td>1791.0</td>
        </tr>
        <tr>
            <td>South Georgia Medical Center</td>
            <td>Valdosta</td>
            <td>GA</td>
            <td>1792.0</td>
        </tr>
        <tr>
            <td>Riverside Shore Memorial Hospital</td>
            <td>Onancock</td>
            <td>VA</td>
            <td>1793.0</td>
        </tr>
        <tr>
            <td>Indiana University Health Arnett Hospital</td>
            <td>Lafayette</td>
            <td>IN</td>
            <td>1794.0</td>
        </tr>
        <tr>
            <td>Vanderbilt Wilson County Hospital</td>
            <td>Lebanon</td>
            <td>TN</td>
            <td>1795.0</td>
        </tr>
        <tr>
            <td>Lehigh Valley Hospital - Hazleton</td>
            <td>Hazleton</td>
            <td>PA</td>
            <td>1796.0</td>
        </tr>
        <tr>
            <td>West Tennessee Healthcare Volunteer Hospital</td>
            <td>Martin</td>
            <td>TN</td>
            <td>1797.0</td>
        </tr>
        <tr>
            <td>Memorial Satilla Health</td>
            <td>Waycross</td>
            <td>GA</td>
            <td>1798.0</td>
        </tr>
        <tr>
            <td>Galesburg Cottage Hospital</td>
            <td>Galesburg</td>
            <td>IL</td>
            <td>1799.0</td>
        </tr>
        <tr>
            <td>South Peninsula Hospital</td>
            <td>Homer</td>
            <td>AK</td>
            <td>1800.0</td>
        </tr>
        <tr>
            <td>Freeman Health System - Freeman West</td>
            <td>Joplin</td>
            <td>MO</td>
            <td>1801.0</td>
        </tr>
        <tr>
            <td>Iredell Memorial Hospital</td>
            <td>Statesville</td>
            <td>NC</td>
            <td>1802.0</td>
        </tr>
        <tr>
            <td>St. Francis Hospital &amp; Medical Center</td>
            <td>Hartford</td>
            <td>CT</td>
            <td>1804.0</td>
        </tr>
        <tr>
            <td>Bates County Memorial Hospital</td>
            <td>Butler</td>
            <td>MO</td>
            <td>1805.0</td>
        </tr>
        <tr>
            <td>Sharon Hospital</td>
            <td>Sharon</td>
            <td>CT</td>
            <td>1806.0</td>
        </tr>
        <tr>
            <td>Littleton Regional Healthcare</td>
            <td>Littleton</td>
            <td>NH</td>
            <td>1807.0</td>
        </tr>
        <tr>
            <td>Parkview Noble Hospital</td>
            <td>Kendallville</td>
            <td>IN</td>
            <td>1808.0</td>
        </tr>
        <tr>
            <td>South Coast Global Medical Center</td>
            <td>Santa Ana</td>
            <td>CA</td>
            <td>1809.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital South</td>
            <td>Saint Louis</td>
            <td>MO</td>
            <td>1810.0</td>
        </tr>
        <tr>
            <td>SSM Health St. Mary&#x27;s Hospital - Jefferson City</td>
            <td>Jefferson City</td>
            <td>MO</td>
            <td>1811.0</td>
        </tr>
        <tr>
            <td>McLaren Port Huron</td>
            <td>Port Huron</td>
            <td>MI</td>
            <td>1812.0</td>
        </tr>
        <tr>
            <td>Cody Regional Health</td>
            <td>Cody</td>
            <td>WY</td>
            <td>1813.0</td>
        </tr>
        <tr>
            <td>Potomac Valley Hospital</td>
            <td>Keyser</td>
            <td>WV</td>
            <td>1814.0</td>
        </tr>
        <tr>
            <td>Lakeview Medical Center Of Rice Lake</td>
            <td>Rice Lake</td>
            <td>WI</td>
            <td>1816.0</td>
        </tr>
        <tr>
            <td>Jewish Hospital - Shelbyville</td>
            <td>Shelbyville</td>
            <td>KY</td>
            <td>1817.0</td>
        </tr>
        <tr>
            <td>University Hospital at Stony Brook</td>
            <td>Stony Brook</td>
            <td>NY</td>
            <td>1818.0</td>
        </tr>
        <tr>
            <td>Medstar Franklin Square Medical Center</td>
            <td>Baltimore</td>
            <td>MD</td>
            <td>1820.0</td>
        </tr>
        <tr>
            <td>Texas Health Harris Methodist Hospital Stephenvill</td>
            <td>Stephenville</td>
            <td>TX</td>
            <td>1821.0</td>
        </tr>
        <tr>
            <td>Thedacare Medical Center - Shawano</td>
            <td>Shawano</td>
            <td>WI</td>
            <td>1822.0</td>
        </tr>
        <tr>
            <td>Sanford Aberdeen Medical Center</td>
            <td>Aberdeen</td>
            <td>SD</td>
            <td>1823.0</td>
        </tr>
        <tr>
            <td>Methodist Hospital</td>
            <td>Henderson</td>
            <td>KY</td>
            <td>1824.0</td>
        </tr>
        <tr>
            <td>Baylor Scott And White Medical Center Mckinney</td>
            <td>Mc Kinney</td>
            <td>TX</td>
            <td>1825.0</td>
        </tr>
        <tr>
            <td>Cascade Valley Hospital</td>
            <td>Arlington</td>
            <td>WA</td>
            <td>1826.0</td>
        </tr>
        <tr>
            <td>Fort Madison Community Hospital</td>
            <td>Fort Madison</td>
            <td>IA</td>
            <td>1827.0</td>
        </tr>
        <tr>
            <td>Brigham City Community Hospital</td>
            <td>Brigham City</td>
            <td>UT</td>
            <td>1828.0</td>
        </tr>
        <tr>
            <td>McLaren Bay Region</td>
            <td>Bay City</td>
            <td>MI</td>
            <td>1829.0</td>
        </tr>
        <tr>
            <td>John Dempsey Hospital</td>
            <td>Farmington</td>
            <td>CT</td>
            <td>1830.0</td>
        </tr>
        <tr>
            <td>Baystate Noble Hospital</td>
            <td>Westfield</td>
            <td>MA</td>
            <td>1831.0</td>
        </tr>
        <tr>
            <td>Ingalls Memorial Hospital</td>
            <td>Harvey</td>
            <td>IL</td>
            <td>1832.0</td>
        </tr>
        <tr>
            <td>Banner Lassen Medical Center</td>
            <td>Susanville</td>
            <td>CA</td>
            <td>1833.0</td>
        </tr>
        <tr>
            <td>Merit Health Madison</td>
            <td>Canton</td>
            <td>MS</td>
            <td>1834.0</td>
        </tr>
        <tr>
            <td>Largo Medical Center</td>
            <td>Largo</td>
            <td>FL</td>
            <td>1835.0</td>
        </tr>
        <tr>
            <td>OhioHealth O&#x27;Bleness Hospital</td>
            <td>Athens</td>
            <td>OH</td>
            <td>1836.0</td>
        </tr>
        <tr>
            <td>Indiana University Health</td>
            <td>Indianapolis</td>
            <td>IN</td>
            <td>1837.0</td>
        </tr>
        <tr>
            <td>Uvalde Memorial Hospital</td>
            <td>Uvalde</td>
            <td>TX</td>
            <td>1838.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Ada</td>
            <td>Ada</td>
            <td>OK</td>
            <td>1839.0</td>
        </tr>
        <tr>
            <td>Lakewood Regional Medical Center</td>
            <td>Lakewood</td>
            <td>CA</td>
            <td>1840.0</td>
        </tr>
        <tr>
            <td>Sycamore Medical Center</td>
            <td>Miamisburg</td>
            <td>OH</td>
            <td>1841.0</td>
        </tr>
        <tr>
            <td>Morton Hospital</td>
            <td>Taunton</td>
            <td>MA</td>
            <td>1843.0</td>
        </tr>
        <tr>
            <td>Owensboro Health Muhlenberg Community Hospital</td>
            <td>Greenville</td>
            <td>KY</td>
            <td>1844.0</td>
        </tr>
        <tr>
            <td>Union Hospital of Cecil County</td>
            <td>Elkton</td>
            <td>MD</td>
            <td>1845.0</td>
        </tr>
        <tr>
            <td>Manchester Memorial Hospital</td>
            <td>Manchester</td>
            <td>CT</td>
            <td>1846.0</td>
        </tr>
        <tr>
            <td>Wamego Health Center</td>
            <td>Wamego</td>
            <td>KS</td>
            <td>1847.0</td>
        </tr>
        <tr>
            <td>Three Rivers Medical Center</td>
            <td>Louisa</td>
            <td>KY</td>
            <td>1848.0</td>
        </tr>
        <tr>
            <td>Integris Baptist Medical Center</td>
            <td>Oklahoma City</td>
            <td>OK</td>
            <td>1849.0</td>
        </tr>
        <tr>
            <td>Jackson Memorial Hospital</td>
            <td>Miami</td>
            <td>FL</td>
            <td>1850.0</td>
        </tr>
        <tr>
            <td>F F Thompson Hospital</td>
            <td>Canandaigua</td>
            <td>NY</td>
            <td>1851.0</td>
        </tr>
        <tr>
            <td>Thedacare Medical Center - Waupaca</td>
            <td>Waupaca</td>
            <td>WI</td>
            <td>1852.0</td>
        </tr>
        <tr>
            <td>West Tennessee Healthcare Dyersburg Hospital</td>
            <td>Dyersburg</td>
            <td>TN</td>
            <td>1854.0</td>
        </tr>
        <tr>
            <td>Frankfort Regional Medical Center</td>
            <td>Frankfort</td>
            <td>KY</td>
            <td>1855.0</td>
        </tr>
        <tr>
            <td>Baptist Memorial Hospital Union County</td>
            <td>New Albany</td>
            <td>MS</td>
            <td>1856.0</td>
        </tr>
        <tr>
            <td>St. Catherine Hospital</td>
            <td>East Chicago</td>
            <td>IN</td>
            <td>1857.0</td>
        </tr>
        <tr>
            <td>Blake Medical Center</td>
            <td>Bradenton</td>
            <td>FL</td>
            <td>1858.0</td>
        </tr>
        <tr>
            <td>Huggins Hospital</td>
            <td>Wolfeboro</td>
            <td>NH</td>
            <td>1859.0</td>
        </tr>
        <tr>
            <td>Swedish American Hospital</td>
            <td>Rockford</td>
            <td>IL</td>
            <td>1860.0</td>
        </tr>
        <tr>
            <td>Lowell General Hospital</td>
            <td>Lowell</td>
            <td>MA</td>
            <td>1861.0</td>
        </tr>
        <tr>
            <td>Grandview Hospital &amp; Medical Center</td>
            <td>Dayton</td>
            <td>OH</td>
            <td>1862.0</td>
        </tr>
        <tr>
            <td>Vidant Chowan Hospital</td>
            <td>Edenton</td>
            <td>NC</td>
            <td>1863.0</td>
        </tr>
        <tr>
            <td>Oswego Hospital</td>
            <td>Oswego</td>
            <td>NY</td>
            <td>1864.0</td>
        </tr>
        <tr>
            <td>Franciscan Health Munster</td>
            <td>Munster</td>
            <td>IN</td>
            <td>1865.0</td>
        </tr>
        <tr>
            <td>Jefferson Healthcare</td>
            <td>Port Townsend</td>
            <td>WA</td>
            <td>1866.0</td>
        </tr>
        <tr>
            <td>Alton Memorial Hospital</td>
            <td>Alton</td>
            <td>IL</td>
            <td>1867.0</td>
        </tr>
        <tr>
            <td>Geisinger-Bloomsburg Hospital</td>
            <td>Bloomsburg</td>
            <td>PA</td>
            <td>1868.0</td>
        </tr>
        <tr>
            <td>Down East Community Hospital</td>
            <td>Machias</td>
            <td>ME</td>
            <td>1869.0</td>
        </tr>
        <tr>
            <td>Beckley ARH Hospital</td>
            <td>Beckley</td>
            <td>WV</td>
            <td>1870.0</td>
        </tr>
        <tr>
            <td>Lakewood Health System</td>
            <td>Staples</td>
            <td>MN</td>
            <td>1871.0</td>
        </tr>
        <tr>
            <td>Southwest Healthcare System</td>
            <td>Murrieta</td>
            <td>CA</td>
            <td>1872.0</td>
        </tr>
        <tr>
            <td>Community Hospital of Bremen</td>
            <td>Bremen</td>
            <td>IN</td>
            <td>1873.0</td>
        </tr>
        <tr>
            <td>Kaweah Delta Medical Center</td>
            <td>Visalia</td>
            <td>CA</td>
            <td>1874.0</td>
        </tr>
        <tr>
            <td>Sagewest Health Care</td>
            <td>Riverton</td>
            <td>WY</td>
            <td>1875.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System-Oakridge</td>
            <td>Osseo</td>
            <td>WI</td>
            <td>1876.0</td>
        </tr>
        <tr>
            <td>Menifee Valley Medical Center</td>
            <td>Sun City</td>
            <td>CA</td>
            <td>1877.0</td>
        </tr>
        <tr>
            <td>Kenmore Mercy Hospital</td>
            <td>Kenmore</td>
            <td>NY</td>
            <td>1878.0</td>
        </tr>
        <tr>
            <td>St. Cloud Regional Medical Center</td>
            <td>Saint Cloud</td>
            <td>FL</td>
            <td>1879.0</td>
        </tr>
        <tr>
            <td>Union Hospital</td>
            <td>Terre Haute</td>
            <td>IN</td>
            <td>1880.0</td>
        </tr>
        <tr>
            <td>The Memorial Hospital</td>
            <td>North Conway</td>
            <td>NH</td>
            <td>1881.0</td>
        </tr>
        <tr>
            <td>Sharp Coronado Hospital</td>
            <td>Coronado</td>
            <td>CA</td>
            <td>1882.0</td>
        </tr>
        <tr>
            <td>The Hospitals of Providence Memorial Campus</td>
            <td>El Paso</td>
            <td>TX</td>
            <td>1883.0</td>
        </tr>
        <tr>
            <td>Union Medical Center</td>
            <td>Union</td>
            <td>SC</td>
            <td>1885.0</td>
        </tr>
        <tr>
            <td>Self Regional Healthcare</td>
            <td>Greenwood</td>
            <td>SC</td>
            <td>1886.0</td>
        </tr>
        <tr>
            <td>Medical Center Hospital</td>
            <td>Odessa</td>
            <td>TX</td>
            <td>1887.0</td>
        </tr>
        <tr>
            <td>Rochelle Community Hospital</td>
            <td>Rochelle</td>
            <td>IL</td>
            <td>1888.0</td>
        </tr>
        <tr>
            <td>Southwestern Vermont Medical Center</td>
            <td>Bennington</td>
            <td>VT</td>
            <td>1889.0</td>
        </tr>
        <tr>
            <td>Jersey City Medical Center</td>
            <td>Jersey City</td>
            <td>NJ</td>
            <td>1890.0</td>
        </tr>
        <tr>
            <td>Pontotoc Health Service Cah</td>
            <td>Pontotoc</td>
            <td>MS</td>
            <td>1891.0</td>
        </tr>
        <tr>
            <td>Ochsner St. Anne General Hospital</td>
            <td>Raceland</td>
            <td>LA</td>
            <td>1892.0</td>
        </tr>
        <tr>
            <td>OSF Saint Lukes Medical Center</td>
            <td>Kewanee</td>
            <td>IL</td>
            <td>1893.0</td>
        </tr>
        <tr>
            <td>Crozer Chester Medical Center</td>
            <td>Upland</td>
            <td>PA</td>
            <td>1894.0</td>
        </tr>
        <tr>
            <td>Riverview Hospital</td>
            <td>Crookston</td>
            <td>MN</td>
            <td>1895.0</td>
        </tr>
        <tr>
            <td>OSF Holy Family Medical Center</td>
            <td>Monmouth</td>
            <td>IL</td>
            <td>1896.0</td>
        </tr>
        <tr>
            <td>Holy Family Hospital</td>
            <td>Methuen</td>
            <td>MA</td>
            <td>1897.0</td>
        </tr>
        <tr>
            <td>Temecula Valley Hospital</td>
            <td>Temecula</td>
            <td>CA</td>
            <td>1898.0</td>
        </tr>
        <tr>
            <td>Medstar Saint Mary&#x27;s Hospital</td>
            <td>Leonardtown</td>
            <td>MD</td>
            <td>1899.0</td>
        </tr>
        <tr>
            <td>DCH Regional Medical Center</td>
            <td>Tuscaloosa</td>
            <td>AL</td>
            <td>1900.0</td>
        </tr>
        <tr>
            <td>Sanford Canby Medical Center</td>
            <td>Canby</td>
            <td>MN</td>
            <td>1901.0</td>
        </tr>
        <tr>
            <td>Southwestern Medical Center</td>
            <td>Lawton</td>
            <td>OK</td>
            <td>1902.0</td>
        </tr>
        <tr>
            <td>Indiana University Health Tipton Hospital</td>
            <td>Tipton</td>
            <td>IN</td>
            <td>1903.0</td>
        </tr>
        <tr>
            <td>IU Health Jay Hospital</td>
            <td>Portland</td>
            <td>IN</td>
            <td>1904.0</td>
        </tr>
        <tr>
            <td>Emanate Health Inter-Community Hospital</td>
            <td>Covina</td>
            <td>CA</td>
            <td>1905.0</td>
        </tr>
        <tr>
            <td>Western Maryland Regional Medical Center</td>
            <td>Cumberland</td>
            <td>MD</td>
            <td>1906.0</td>
        </tr>
        <tr>
            <td>Graham Hospital Association</td>
            <td>Canton</td>
            <td>IL</td>
            <td>1907.0</td>
        </tr>
        <tr>
            <td>Martin Luther King, Jr. Community Hospital</td>
            <td>Los Angeles</td>
            <td>CA</td>
            <td>1908.0</td>
        </tr>
        <tr>
            <td>Regional Medical Center</td>
            <td>Manchester</td>
            <td>IA</td>
            <td>1909.0</td>
        </tr>
        <tr>
            <td>Carolina Pines Regional Medical Center</td>
            <td>Hartsville</td>
            <td>SC</td>
            <td>1910.0</td>
        </tr>
        <tr>
            <td>Desert Regional Medical Center</td>
            <td>Palm Springs</td>
            <td>CA</td>
            <td>1911.0</td>
        </tr>
        <tr>
            <td>Arnot Ogden Medical Center</td>
            <td>Elmira</td>
            <td>NY</td>
            <td>1912.0</td>
        </tr>
        <tr>
            <td>Dukes Memorial Hospital</td>
            <td>Peru</td>
            <td>IN</td>
            <td>1913.0</td>
        </tr>
        <tr>
            <td>St. Elizabeth Medical Center</td>
            <td>Wabasha</td>
            <td>MN</td>
            <td>1914.0</td>
        </tr>
        <tr>
            <td>Christus Good Shepherd Medical Center Marshall</td>
            <td>Marshall</td>
            <td>TX</td>
            <td>1915.0</td>
        </tr>
        <tr>
            <td>Morton Plant North Bay Hospital</td>
            <td>New Port Richey</td>
            <td>FL</td>
            <td>1916.0</td>
        </tr>
        <tr>
            <td>Wyoming Medical Center</td>
            <td>Casper</td>
            <td>WY</td>
            <td>1917.0</td>
        </tr>
        <tr>
            <td>Boulder City Hospital</td>
            <td>Boulder City</td>
            <td>NV</td>
            <td>1918.0</td>
        </tr>
        <tr>
            <td>Sunnyside Community Hospital</td>
            <td>Sunnyside</td>
            <td>WA</td>
            <td>1919.0</td>
        </tr>
        <tr>
            <td>Madison Health</td>
            <td>London</td>
            <td>OH</td>
            <td>1920.0</td>
        </tr>
        <tr>
            <td>JFK Medical Center - Anthony M. Yelencsics Community</td>
            <td>Edison</td>
            <td>NJ</td>
            <td>1921.0</td>
        </tr>
        <tr>
            <td>Baptist Health Medical Center-Little Rock</td>
            <td>Little Rock</td>
            <td>AR</td>
            <td>1922.0</td>
        </tr>
        <tr>
            <td>Maria Parham Medical Center</td>
            <td>Henderson</td>
            <td>NC</td>
            <td>1923.0</td>
        </tr>
        <tr>
            <td>Harney District Hospital</td>
            <td>Burns</td>
            <td>OR</td>
            <td>1924.0</td>
        </tr>
        <tr>
            <td>Mary Greeley Medical Center</td>
            <td>Ames</td>
            <td>IA</td>
            <td>1925.0</td>
        </tr>
        <tr>
            <td>Woodlawn Hospital</td>
            <td>Rochester</td>
            <td>IN</td>
            <td>1927.0</td>
        </tr>
        <tr>
            <td>Ridgecrest Regional Hospital</td>
            <td>Ridgecrest</td>
            <td>CA</td>
            <td>1928.0</td>
        </tr>
        <tr>
            <td>University Hospital Mcduffie</td>
            <td>Thomson</td>
            <td>GA</td>
            <td>1929.0</td>
        </tr>
        <tr>
            <td>Doctors Hospital Of Sarasota</td>
            <td>Sarasota</td>
            <td>FL</td>
            <td>1930.0</td>
        </tr>
        <tr>
            <td>Vaughan Regional Medical Center Parkway Campus</td>
            <td>Selma</td>
            <td>AL</td>
            <td>1931.0</td>
        </tr>
        <tr>
            <td>Bon Secours Community Hospital</td>
            <td>Port Jervis</td>
            <td>NY</td>
            <td>1932.0</td>
        </tr>
        <tr>
            <td>Northern Inyo Hospital</td>
            <td>Bishop</td>
            <td>CA</td>
            <td>1933.0</td>
        </tr>
        <tr>
            <td>St. Peters Hospital</td>
            <td>Helena</td>
            <td>MT</td>
            <td>1934.0</td>
        </tr>
        <tr>
            <td>Gothenburg Memorial Hospital</td>
            <td>Gothenburg</td>
            <td>NE</td>
            <td>1935.0</td>
        </tr>
        <tr>
            <td>Massac Memorial Hospital</td>
            <td>Metropolis</td>
            <td>IL</td>
            <td>1936.0</td>
        </tr>
        <tr>
            <td>Taylorville Memorial Hospital</td>
            <td>Taylorville</td>
            <td>IL</td>
            <td>1937.0</td>
        </tr>
        <tr>
            <td>Greenview Regional Hospital</td>
            <td>Bowling Green</td>
            <td>KY</td>
            <td>1938.0</td>
        </tr>
        <tr>
            <td>Our Lady of the Lake Regional Medical Center</td>
            <td>Baton Rouge</td>
            <td>LA</td>
            <td>1939.0</td>
        </tr>
        <tr>
            <td>Sanford Medical Center Thief River Falls</td>
            <td>Thief River Falls</td>
            <td>MN</td>
            <td>1940.0</td>
        </tr>
        <tr>
            <td>Community Hospitals and Wellness Centers</td>
            <td>Bryan</td>
            <td>OH</td>
            <td>1941.0</td>
        </tr>
        <tr>
            <td>Fairfield Medical Center</td>
            <td>Lancaster</td>
            <td>OH</td>
            <td>1942.0</td>
        </tr>
        <tr>
            <td>Novant Health Thomasville Medical Center</td>
            <td>Thomasville</td>
            <td>NC</td>
            <td>1943.0</td>
        </tr>
        <tr>
            <td>Fitzgibbon Hospital</td>
            <td>Marshall</td>
            <td>MO</td>
            <td>1944.0</td>
        </tr>
        <tr>
            <td>Chapman Global Medical Center</td>
            <td>Orange</td>
            <td>CA</td>
            <td>1945.0</td>
        </tr>
        <tr>
            <td>Abington Memorial Hospital</td>
            <td>Abington</td>
            <td>PA</td>
            <td>1946.0</td>
        </tr>
        <tr>
            <td>Providence Health</td>
            <td>Columbia</td>
            <td>SC</td>
            <td>1947.0</td>
        </tr>
        <tr>
            <td>East Georgia Regional Medical Center</td>
            <td>Statesboro</td>
            <td>GA</td>
            <td>1948.0</td>
        </tr>
        <tr>
            <td>Essentia Health Sandstone</td>
            <td>Sandstone</td>
            <td>MN</td>
            <td>1949.0</td>
        </tr>
        <tr>
            <td>Lincoln Medical Center</td>
            <td>Fayetteville</td>
            <td>TN</td>
            <td>1950.0</td>
        </tr>
        <tr>
            <td>Virtua Memorial Hospital of Burlington County</td>
            <td>Mount Holly</td>
            <td>NJ</td>
            <td>1951.0</td>
        </tr>
        <tr>
            <td>Ohio Valley General Hospital</td>
            <td>McKees Rocks</td>
            <td>PA</td>
            <td>1952.0</td>
        </tr>
        <tr>
            <td>Platte Health Center - Cah</td>
            <td>Platte</td>
            <td>SD</td>
            <td>1953.0</td>
        </tr>
        <tr>
            <td>Midland Memorial Hospital</td>
            <td>Midland</td>
            <td>TX</td>
            <td>1954.0</td>
        </tr>
        <tr>
            <td>Chambers Memorial Hospital</td>
            <td>Danville</td>
            <td>AR</td>
            <td>1955.0</td>
        </tr>
        <tr>
            <td>Northern Light A.R. Gould Hospital</td>
            <td>Presque Isle</td>
            <td>ME</td>
            <td>1956.0</td>
        </tr>
        <tr>
            <td>Saint Alphonsus Medical Center - Baker City</td>
            <td>Baker City</td>
            <td>OR</td>
            <td>1957.0</td>
        </tr>
        <tr>
            <td>Mercy Health - Urbana Hospital</td>
            <td>Urbana</td>
            <td>OH</td>
            <td>1958.0</td>
        </tr>
        <tr>
            <td>UPMC Chautauqua</td>
            <td>Jamestown</td>
            <td>NY</td>
            <td>1959.0</td>
        </tr>
        <tr>
            <td>Bakersfield Memorial Hospital</td>
            <td>Bakersfield</td>
            <td>CA</td>
            <td>1960.0</td>
        </tr>
        <tr>
            <td>Macon Community Hospital</td>
            <td>Lafayette</td>
            <td>TN</td>
            <td>1961.0</td>
        </tr>
        <tr>
            <td>Eastland Memorial Hospital</td>
            <td>Eastland</td>
            <td>TX</td>
            <td>1963.0</td>
        </tr>
        <tr>
            <td>Grundy County Memorial Hospital</td>
            <td>Grundy Center</td>
            <td>IA</td>
            <td>1964.0</td>
        </tr>
        <tr>
            <td>OSF Sacred Heart Medical Center</td>
            <td>Danville</td>
            <td>IL</td>
            <td>1965.0</td>
        </tr>
        <tr>
            <td>Takoma Regional Hospital</td>
            <td>Greeneville</td>
            <td>TN</td>
            <td>1966.0</td>
        </tr>
        <tr>
            <td>Lane Regional Medical Center</td>
            <td>Zachary</td>
            <td>LA</td>
            <td>1967.0</td>
        </tr>
        <tr>
            <td>Northeast Georgia Medical Center Barrow</td>
            <td>Winder</td>
            <td>GA</td>
            <td>1968.0</td>
        </tr>
        <tr>
            <td>Herrin Hospital</td>
            <td>Herrin</td>
            <td>IL</td>
            <td>1969.0</td>
        </tr>
        <tr>
            <td>Pender Memorial Hospital</td>
            <td>Burgaw</td>
            <td>NC</td>
            <td>1970.0</td>
        </tr>
        <tr>
            <td>Mount Desert Island Hospital</td>
            <td>Bar Harbor</td>
            <td>ME</td>
            <td>1971.0</td>
        </tr>
        <tr>
            <td>Cox Medical Centers</td>
            <td>Springfield</td>
            <td>MO</td>
            <td>1972.0</td>
        </tr>
        <tr>
            <td>Wallowa Memorial Hospital</td>
            <td>Enterprise</td>
            <td>OR</td>
            <td>1973.0</td>
        </tr>
        <tr>
            <td>Unicoi CountyÂ¬â€  Hospital</td>
            <td>Erwin</td>
            <td>TN</td>
            <td>1974.0</td>
        </tr>
        <tr>
            <td>Englewood Hospital and Medical Center</td>
            <td>Englewood</td>
            <td>NJ</td>
            <td>1975.0</td>
        </tr>
        <tr>
            <td>St. Mary&#x27;s Sacred Heart Hospital</td>
            <td>Lavonia</td>
            <td>GA</td>
            <td>1976.0</td>
        </tr>
        <tr>
            <td>Merit Health River Region</td>
            <td>Vicksburg</td>
            <td>MS</td>
            <td>1977.0</td>
        </tr>
        <tr>
            <td>PeaceHealth United General Medical Center</td>
            <td>Sedro Woolley</td>
            <td>WA</td>
            <td>1978.0</td>
        </tr>
        <tr>
            <td>Ocean Beach Hospital</td>
            <td>Ilwaco</td>
            <td>WA</td>
            <td>1979.0</td>
        </tr>
        <tr>
            <td>Coffeyville Regional Medical Center</td>
            <td>Coffeyville</td>
            <td>KS</td>
            <td>1980.0</td>
        </tr>
        <tr>
            <td>Salina Regional Health Center</td>
            <td>Salina</td>
            <td>KS</td>
            <td>1982.0</td>
        </tr>
        <tr>
            <td>Baptist Memorial Hospital Golden Triangle</td>
            <td>Columbus</td>
            <td>MS</td>
            <td>1983.0</td>
        </tr>
        <tr>
            <td>Hampshire Memorial Hospital</td>
            <td>Romney</td>
            <td>WV</td>
            <td>1984.0</td>
        </tr>
        <tr>
            <td>Cuero Regional Hospital</td>
            <td>Cuero</td>
            <td>TX</td>
            <td>1985.0</td>
        </tr>
        <tr>
            <td>Baptist Memorial Hospital Booneville</td>
            <td>Booneville</td>
            <td>MS</td>
            <td>1986.0</td>
        </tr>
        <tr>
            <td>Northern Light Maine Coast Hospital</td>
            <td>Ellsworth</td>
            <td>ME</td>
            <td>1987.0</td>
        </tr>
        <tr>
            <td>Saint Thomas Dekalb Hospital</td>
            <td>Smithville</td>
            <td>TN</td>
            <td>1989.0</td>
        </tr>
        <tr>
            <td>Highlands Hospital</td>
            <td>Connellsville</td>
            <td>PA</td>
            <td>1990.0</td>
        </tr>
        <tr>
            <td>Vidant BertieÂ¬â€  Hospital</td>
            <td>Windsor</td>
            <td>NC</td>
            <td>1991.0</td>
        </tr>
        <tr>
            <td>Lea Regional Medical Center</td>
            <td>Hobbs</td>
            <td>NM</td>
            <td>1992.0</td>
        </tr>
        <tr>
            <td>Mayo Regional Hospital</td>
            <td>Dover Foxcroft</td>
            <td>ME</td>
            <td>1993.0</td>
        </tr>
        <tr>
            <td>Indiana University Health Blackford Hospital</td>
            <td>Hartford City</td>
            <td>IN</td>
            <td>1994.0</td>
        </tr>
        <tr>
            <td>Eastern New Mexico Medical Center</td>
            <td>Roswell</td>
            <td>NM</td>
            <td>1995.0</td>
        </tr>
        <tr>
            <td>Divine Savior Healthcare</td>
            <td>Portage</td>
            <td>WI</td>
            <td>1996.0</td>
        </tr>
        <tr>
            <td>North Valley Hospital</td>
            <td>Whitefish</td>
            <td>MT</td>
            <td>1997.0</td>
        </tr>
        <tr>
            <td>Upland Hills Health</td>
            <td>Dodgeville</td>
            <td>WI</td>
            <td>1998.0</td>
        </tr>
        <tr>
            <td>The Hospitals Of Providence Transmountain Campus</td>
            <td>El Paso</td>
            <td>TX</td>
            <td>1999.0</td>
        </tr>
        <tr>
            <td>Spooner Health System</td>
            <td>Spooner</td>
            <td>WI</td>
            <td>2001.0</td>
        </tr>
        <tr>
            <td>Lawrence Medical Center</td>
            <td>Moulton</td>
            <td>AL</td>
            <td>2002.0</td>
        </tr>
        <tr>
            <td>Mcleod Health Clarendon</td>
            <td>Manning</td>
            <td>SC</td>
            <td>2003.0</td>
        </tr>
        <tr>
            <td>Holy Family Memorial</td>
            <td>Manitowoc</td>
            <td>WI</td>
            <td>2004.0</td>
        </tr>
        <tr>
            <td>Sebasticook Valley Health</td>
            <td>Pittsfield</td>
            <td>ME</td>
            <td>2005.0</td>
        </tr>
        <tr>
            <td>Baptist Health Medical Center-Hot Springs County</td>
            <td>Malvern</td>
            <td>AR</td>
            <td>2006.0</td>
        </tr>
        <tr>
            <td>Odessa Regional Medical Center</td>
            <td>Odessa</td>
            <td>TX</td>
            <td>2007.0</td>
        </tr>
        <tr>
            <td>Integris Grove Hospital</td>
            <td>Grove</td>
            <td>OK</td>
            <td>2008.0</td>
        </tr>
        <tr>
            <td>Christus Spohn Hospital Kleberg</td>
            <td>Kingsville</td>
            <td>TX</td>
            <td>2009.0</td>
        </tr>
        <tr>
            <td>Hoopeston Community Memorial Hospital</td>
            <td>Hoopeston</td>
            <td>IL</td>
            <td>2010.0</td>
        </tr>
        <tr>
            <td>Purcell Municipal Hospital</td>
            <td>Purcell</td>
            <td>OK</td>
            <td>2011.0</td>
        </tr>
        <tr>
            <td>Cabinet Peaks Medical Center</td>
            <td>Libby</td>
            <td>MT</td>
            <td>2012.0</td>
        </tr>
        <tr>
            <td>Cogdell Memorial Hospital</td>
            <td>Snyder</td>
            <td>TX</td>
            <td>2013.0</td>
        </tr>
        <tr>
            <td>University Hospital &amp; Clinics</td>
            <td>Lafayette</td>
            <td>LA</td>
            <td>2014.0</td>
        </tr>
        <tr>
            <td>Scenic Mountain Medical Center</td>
            <td>Big Spring</td>
            <td>TX</td>
            <td>2015.0</td>
        </tr>
        <tr>
            <td>Desoto Memorial Hospital</td>
            <td>Arcadia</td>
            <td>FL</td>
            <td>2016.0</td>
        </tr>
        <tr>
            <td>Alta Vista Regional Hospital</td>
            <td>Las Vegas</td>
            <td>NM</td>
            <td>2017.0</td>
        </tr>
        <tr>
            <td>Logan Regional Medical Center</td>
            <td>Logan</td>
            <td>WV</td>
            <td>2018.0</td>
        </tr>
        <tr>
            <td>Baptist Memorial Hospital Tipton</td>
            <td>Covington</td>
            <td>TN</td>
            <td>2019.0</td>
        </tr>
        <tr>
            <td>Hampton Regional Medical Center</td>
            <td>Varnville</td>
            <td>SC</td>
            <td>2020.0</td>
        </tr>
        <tr>
            <td>Tawas St. Joseph Hospital</td>
            <td>Tawas City</td>
            <td>MI</td>
            <td>2021.0</td>
        </tr>
        <tr>
            <td>AllianceHealth Durant</td>
            <td>Durant</td>
            <td>OK</td>
            <td>2022.0</td>
        </tr>
        <tr>
            <td>Beth Israel Deaconess Hospital - Needham</td>
            <td>Needham</td>
            <td>MA</td>
            <td>2023.0</td>
        </tr>
        <tr>
            <td>Marshfield Medical Center - Ladysmith</td>
            <td>Ladysmith</td>
            <td>WI</td>
            <td>2024.0</td>
        </tr>
        <tr>
            <td>Christus Spohn Hospital Alice</td>
            <td>Alice</td>
            <td>TX</td>
            <td>2025.0</td>
        </tr>
        <tr>
            <td>Yoakum County Hospital</td>
            <td>Denver City</td>
            <td>TX</td>
            <td>2026.0</td>
        </tr>
        <tr>
            <td>Limestone Medical Center</td>
            <td>Groesbeck</td>
            <td>TX</td>
            <td>2027.0</td>
        </tr>
        <tr>
            <td>San Juan Hospital</td>
            <td>Monticello</td>
            <td>UT</td>
            <td>2028.0</td>
        </tr>
        <tr>
            <td>Grant Memorial Hospital</td>
            <td>Petersburg</td>
            <td>WV</td>
            <td>2031.0</td>
        </tr>
        <tr>
            <td>Pulaski Memorial Hospital</td>
            <td>Winamac</td>
            <td>IN</td>
            <td>2032.0</td>
        </tr>
        <tr>
            <td>Door County Medical Center</td>
            <td>Sturgeon Bay</td>
            <td>WI</td>
            <td>2033.0</td>
        </tr>
        <tr>
            <td>Millcreek Community Hospital</td>
            <td>Erie</td>
            <td>PA</td>
            <td>2034.0</td>
        </tr>
        <tr>
            <td>Three Rivers Health</td>
            <td>Three Rivers</td>
            <td>MI</td>
            <td>2035.0</td>
        </tr>
        <tr>
            <td>South Central Reg Medical Center</td>
            <td>Laurel</td>
            <td>MS</td>
            <td>2036.0</td>
        </tr>
        <tr>
            <td>Massena Memorial Hospital</td>
            <td>Massena</td>
            <td>NY</td>
            <td>2037.0</td>
        </tr>
        <tr>
            <td>Spring Valley Hospital Medical Center</td>
            <td>Las Vegas</td>
            <td>NV</td>
            <td>2038.0</td>
        </tr>
        <tr>
            <td>North Texas Medical Center</td>
            <td>Gainesville</td>
            <td>TX</td>
            <td>2039.0</td>
        </tr>
        <tr>
            <td>Kane Community Hospital</td>
            <td>Kane</td>
            <td>PA</td>
            <td>2040.0</td>
        </tr>
        <tr>
            <td>Drew Memorial Hospital</td>
            <td>Monticello</td>
            <td>AR</td>
            <td>2041.0</td>
        </tr>
        <tr>
            <td>Taylor Regional Hospital</td>
            <td>Hawkinsville</td>
            <td>GA</td>
            <td>2043.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Booneville</td>
            <td>Booneville</td>
            <td>AR</td>
            <td>2044.0</td>
        </tr>
        <tr>
            <td>Willapa Harbor Hospital</td>
            <td>South Bend</td>
            <td>WA</td>
            <td>2045.0</td>
        </tr>
        <tr>
            <td>UT Health East Texas Henderson Hospital</td>
            <td>Henderson</td>
            <td>TX</td>
            <td>2047.0</td>
        </tr>
        <tr>
            <td>Johnson Regional Medical Center</td>
            <td>Clarksville</td>
            <td>AR</td>
            <td>2048.0</td>
        </tr>
        <tr>
            <td>Franciscan Health Rensselaer</td>
            <td>Rensselaer</td>
            <td>IN</td>
            <td>2050.0</td>
        </tr>
        <tr>
            <td>Paul B Hall Regional Medical Center</td>
            <td>Paintsville</td>
            <td>KY</td>
            <td>2051.0</td>
        </tr>
        <tr>
            <td>Opelousas General Health System</td>
            <td>Opelousas</td>
            <td>LA</td>
            <td>2052.0</td>
        </tr>
        <tr>
            <td>Henry County Hospital</td>
            <td>Napoleon</td>
            <td>OH</td>
            <td>2053.0</td>
        </tr>
        <tr>
            <td>Blackwell Regional Hospital</td>
            <td>Blackwell</td>
            <td>OK</td>
            <td>2054.0</td>
        </tr>
        <tr>
            <td>Holzer Medical Center Jackson</td>
            <td>Jackson</td>
            <td>OH</td>
            <td>2055.0</td>
        </tr>
        <tr>
            <td>University of Mississippi Medical Center- Grenada</td>
            <td>Grenada</td>
            <td>MS</td>
            <td>2056.0</td>
        </tr>
        <tr>
            <td>Missouri Delta Medical Center</td>
            <td>Sikeston</td>
            <td>MO</td>
            <td>2057.0</td>
        </tr>
        <tr>
            <td>Aultman Orrville Hospital</td>
            <td>Orrville</td>
            <td>OH</td>
            <td>2058.0</td>
        </tr>
        <tr>
            <td>North Oaks Medical Center</td>
            <td>Hammond</td>
            <td>LA</td>
            <td>2059.0</td>
        </tr>
        <tr>
            <td>Permian Regional Medical Center Andrews County Hospital</td>
            <td>Andrews</td>
            <td>TX</td>
            <td>2060.0</td>
        </tr>
        <tr>
            <td>Perry Memorial Hospital</td>
            <td>Princeton</td>
            <td>IL</td>
            <td>2061.0</td>
        </tr>
        <tr>
            <td>CHI Health St. Mary&#x27;s</td>
            <td>Nebraska City</td>
            <td>NE</td>
            <td>2062.0</td>
        </tr>
        <tr>
            <td>East Ohio Regional Hospital</td>
            <td>Martins Ferry</td>
            <td>OH</td>
            <td>2063.0</td>
        </tr>
        <tr>
            <td>Twin Lakes Regional Medical Center</td>
            <td>Leitchfield</td>
            <td>KY</td>
            <td>2064.0</td>
        </tr>
        <tr>
            <td>Klickitat Valley Hospital</td>
            <td>Goldendale</td>
            <td>WA</td>
            <td>2065.0</td>
        </tr>
        <tr>
            <td>Evans Memorial Hospital</td>
            <td>Claxton</td>
            <td>GA</td>
            <td>2066.0</td>
        </tr>
        <tr>
            <td>Pecos County Memorial Hospital</td>
            <td>Fort Stockton</td>
            <td>TX</td>
            <td>2067.0</td>
        </tr>
        <tr>
            <td>Sparks Medical Center - Van Buren</td>
            <td>Van Buren</td>
            <td>AR</td>
            <td>2068.0</td>
        </tr>
        <tr>
            <td>Medstar Washington Hospital Center</td>
            <td>Washington</td>
            <td>DC</td>
            <td>2069.0</td>
        </tr>
        <tr>
            <td>Presence Saints Mary and Elizabeth Medical Center</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>2070.0</td>
        </tr>
        <tr>
            <td>University of Illinois Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>2071.0</td>
        </tr>
        <tr>
            <td>West Suburban Medical Center</td>
            <td>Oak Park</td>
            <td>IL</td>
            <td>2072.0</td>
        </tr>
        <tr>
            <td>Atlanticare Regional Medical Center - City Campus</td>
            <td>Atlantic City</td>
            <td>NJ</td>
            <td>2073.0</td>
        </tr>
        <tr>
            <td>Carney Hospital</td>
            <td>Boston</td>
            <td>MA</td>
            <td>2074.0</td>
        </tr>
        <tr>
            <td>York Hospital</td>
            <td>York</td>
            <td>ME</td>
            <td>2075.0</td>
        </tr>
        <tr>
            <td>Toppenish Community Hospital</td>
            <td>Toppenish</td>
            <td>WA</td>
            <td>2076.0</td>
        </tr>
        <tr>
            <td>Fountain Valley Regional Hospital &amp; Medical Center</td>
            <td>Fountain Valley</td>
            <td>CA</td>
            <td>2077.0</td>
        </tr>
        <tr>
            <td>Albert Einstein Medical Center</td>
            <td>Philadelphia</td>
            <td>PA</td>
            <td>2078.0</td>
        </tr>
        <tr>
            <td>Emory Decatur Hospital</td>
            <td>Decatur</td>
            <td>GA</td>
            <td>2079.0</td>
        </tr>
        <tr>
            <td>Aultman Hospital</td>
            <td>Canton</td>
            <td>OH</td>
            <td>2080.0</td>
        </tr>
        <tr>
            <td>Regional West Medical Center</td>
            <td>Scottsbluff</td>
            <td>NE</td>
            <td>2081.0</td>
        </tr>
        <tr>
            <td>Candler Hospital</td>
            <td>Savannah</td>
            <td>GA</td>
            <td>2082.0</td>
        </tr>
        <tr>
            <td>Coney Island Hospital</td>
            <td>Brooklyn</td>
            <td>NY</td>
            <td>2083.0</td>
        </tr>
        <tr>
            <td>Mary Washington Hospital</td>
            <td>Fredericksburg</td>
            <td>VA</td>
            <td>2084.0</td>
        </tr>
        <tr>
            <td>University Medical Center New Orleans</td>
            <td>New Orleans</td>
            <td>LA</td>
            <td>2085.0</td>
        </tr>
        <tr>
            <td>St. Joseph&#x27;s University Medical Center</td>
            <td>Paterson</td>
            <td>NJ</td>
            <td>2086.0</td>
        </tr>
        <tr>
            <td>College Medical Center</td>
            <td>Long Beach</td>
            <td>CA</td>
            <td>2087.0</td>
        </tr>
        <tr>
            <td>Monmouth Medical Center-Southern Campus</td>
            <td>Lakewood</td>
            <td>NJ</td>
            <td>2088.0</td>
        </tr>
        <tr>
            <td>Health Alliance - Clinton Hospital</td>
            <td>Leominster</td>
            <td>MA</td>
            <td>2089.0</td>
        </tr>
        <tr>
            <td>Heywood Hospital</td>
            <td>Gardner</td>
            <td>MA</td>
            <td>2090.0</td>
        </tr>
        <tr>
            <td>Madera Community Hospital</td>
            <td>Madera</td>
            <td>CA</td>
            <td>2091.0</td>
        </tr>
        <tr>
            <td>St. Lukes Regional Medical Center</td>
            <td>Sioux City</td>
            <td>IA</td>
            <td>2092.0</td>
        </tr>
        <tr>
            <td>East Los Angeles Doctors Hospital</td>
            <td>Los Angeles</td>
            <td>CA</td>
            <td>2093.0</td>
        </tr>
        <tr>
            <td>Signature Healthcare Brockton Hospital</td>
            <td>Brockton</td>
            <td>MA</td>
            <td>2094.0</td>
        </tr>
        <tr>
            <td>Plains Regional Medical Center</td>
            <td>Clovis</td>
            <td>NM</td>
            <td>2095.0</td>
        </tr>
        <tr>
            <td>Onslow Memorial Hospital</td>
            <td>Jacksonville</td>
            <td>NC</td>
            <td>2096.0</td>
        </tr>
        <tr>
            <td>Spartanburg Medical Center</td>
            <td>Spartanburg</td>
            <td>SC</td>
            <td>2097.0</td>
        </tr>
        <tr>
            <td>Flushing Hospital Medical Center</td>
            <td>Flushing</td>
            <td>NY</td>
            <td>2098.0</td>
        </tr>
        <tr>
            <td>Piedmont Rockdale Hospital</td>
            <td>Conyers</td>
            <td>GA</td>
            <td>2099.0</td>
        </tr>
        <tr>
            <td>Ventura County Medical Center</td>
            <td>Ventura</td>
            <td>CA</td>
            <td>2100.0</td>
        </tr>
        <tr>
            <td>Franciscan Health Hammond</td>
            <td>Hammond</td>
            <td>IN</td>
            <td>2101.0</td>
        </tr>
        <tr>
            <td>Wellstar Spalding Regional Hospital</td>
            <td>Griffin</td>
            <td>GA</td>
            <td>2102.0</td>
        </tr>
        <tr>
            <td>Watsonville Community Hospital</td>
            <td>Watsonville</td>
            <td>CA</td>
            <td>2103.0</td>
        </tr>
        <tr>
            <td>UAMS Medical Center</td>
            <td>Little Rock</td>
            <td>AR</td>
            <td>2104.0</td>
        </tr>
        <tr>
            <td>Hca Houston Healthcare Pearland</td>
            <td>Pearland</td>
            <td>TX</td>
            <td>2105.0</td>
        </tr>
        <tr>
            <td>Grays Harbor Community Hospital</td>
            <td>Aberdeen</td>
            <td>WA</td>
            <td>2106.0</td>
        </tr>
        <tr>
            <td>East Orange General Hospital</td>
            <td>East Orange</td>
            <td>NJ</td>
            <td>2107.0</td>
        </tr>
        <tr>
            <td>Citizens Baptist Medical Center</td>
            <td>Talladega</td>
            <td>AL</td>
            <td>2108.0</td>
        </tr>
        <tr>
            <td>Antelope Valley Hospital</td>
            <td>Lancaster</td>
            <td>CA</td>
            <td>2109.0</td>
        </tr>
        <tr>
            <td>United Health Services Hospitals</td>
            <td>Binghamton</td>
            <td>NY</td>
            <td>2110.0</td>
        </tr>
        <tr>
            <td>TRMC of Orangeburg &amp; Calhoun</td>
            <td>Orangeburg</td>
            <td>SC</td>
            <td>2111.0</td>
        </tr>
        <tr>
            <td>Loretto Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>2112.0</td>
        </tr>
        <tr>
            <td>OU Medicine</td>
            <td>Oklahoma City</td>
            <td>OK</td>
            <td>2113.0</td>
        </tr>
        <tr>
            <td>Maimonides Medical Center</td>
            <td>Brooklyn</td>
            <td>NY</td>
            <td>2114.0</td>
        </tr>
        <tr>
            <td>AU Medical Center</td>
            <td>Augusta</td>
            <td>GA</td>
            <td>2115.0</td>
        </tr>
        <tr>
            <td>Salem Medical Center</td>
            <td>Salem</td>
            <td>NJ</td>
            <td>2116.0</td>
        </tr>
        <tr>
            <td>St. Bernard Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>2117.0</td>
        </tr>
        <tr>
            <td>Anaheim Global Medical Center</td>
            <td>Anaheim</td>
            <td>CA</td>
            <td>2119.0</td>
        </tr>
        <tr>
            <td>SSM Health St. Anthony Hospital - Shawnee</td>
            <td>Shawnee</td>
            <td>OK</td>
            <td>2120.0</td>
        </tr>
        <tr>
            <td>Long Island Community Hospital</td>
            <td>Patchogue</td>
            <td>NY</td>
            <td>2121.0</td>
        </tr>
        <tr>
            <td>Fairbanks Memorial Hospital</td>
            <td>Fairbanks</td>
            <td>AK</td>
            <td>2122.0</td>
        </tr>
        <tr>
            <td>Cooper University Hospital</td>
            <td>Camden</td>
            <td>NJ</td>
            <td>2123.0</td>
        </tr>
        <tr>
            <td>Rollins Brook Community Hospital</td>
            <td>Lampasas</td>
            <td>TX</td>
            <td>2125.0</td>
        </tr>
        <tr>
            <td>Tippah County Hospital</td>
            <td>Ripley</td>
            <td>MS</td>
            <td>2127.0</td>
        </tr>
        <tr>
            <td>Gifford Medical Center</td>
            <td>Randolph</td>
            <td>VT</td>
            <td>2128.0</td>
        </tr>
        <tr>
            <td>Ward Memorial Hospital</td>
            <td>Monahans</td>
            <td>TX</td>
            <td>2129.0</td>
        </tr>
        <tr>
            <td>Lake City Community Hospital</td>
            <td>Lake City</td>
            <td>SC</td>
            <td>2130.0</td>
        </tr>
        <tr>
            <td>Atrium Health Anson</td>
            <td>Wadesboro</td>
            <td>NC</td>
            <td>2131.0</td>
        </tr>
        <tr>
            <td>New York Community Hospital of Brooklyn</td>
            <td>Brooklyn</td>
            <td>NY</td>
            <td>2132.0</td>
        </tr>
        <tr>
            <td>Mayers Memorial Hospital</td>
            <td>Fall River Mills</td>
            <td>CA</td>
            <td>2133.0</td>
        </tr>
        <tr>
            <td>Winner Regional Healthcare Center</td>
            <td>Winner</td>
            <td>SD</td>
            <td>2134.0</td>
        </tr>
        <tr>
            <td>San Joaquin General Hospital</td>
            <td>French Camp</td>
            <td>CA</td>
            <td>2135.0</td>
        </tr>
        <tr>
            <td>Thorek Memorial Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>2136.0</td>
        </tr>
        <tr>
            <td>Kossuth Regional Health Center</td>
            <td>Algona</td>
            <td>IA</td>
            <td>2137.0</td>
        </tr>
        <tr>
            <td>Summers County ARH Hospital</td>
            <td>Hinton</td>
            <td>WV</td>
            <td>2138.0</td>
        </tr>
        <tr>
            <td>Nicholas H Noyes Memorial Hospital</td>
            <td>Dansville</td>
            <td>NY</td>
            <td>2139.0</td>
        </tr>
        <tr>
            <td>Bob Wilson Memorial Grant County Hospital</td>
            <td>Ulysses</td>
            <td>KS</td>
            <td>2140.0</td>
        </tr>
        <tr>
            <td>Franklin Foundation Hospital</td>
            <td>Franklin</td>
            <td>LA</td>
            <td>2141.0</td>
        </tr>
        <tr>
            <td>AllianceHealth Seminole</td>
            <td>Seminole</td>
            <td>OK</td>
            <td>2142.0</td>
        </tr>
        <tr>
            <td>Indiana University Health Paoli Hospital</td>
            <td>Paoli</td>
            <td>IN</td>
            <td>2143.0</td>
        </tr>
        <tr>
            <td>Claiborne Memorial Medical Center</td>
            <td>Homer</td>
            <td>LA</td>
            <td>2144.0</td>
        </tr>
        <tr>
            <td>South Mississippi County Regional Medical Center</td>
            <td>Osceola</td>
            <td>AR</td>
            <td>2145.0</td>
        </tr>
        <tr>
            <td>Ballinger Memorial Hospital</td>
            <td>Ballinger</td>
            <td>TX</td>
            <td>2146.0</td>
        </tr>
        <tr>
            <td>Newberry County Memorial Hospital</td>
            <td>Newberry</td>
            <td>SC</td>
            <td>2147.0</td>
        </tr>
        <tr>
            <td>Putnam County Hospital</td>
            <td>Greencastle</td>
            <td>IN</td>
            <td>2148.0</td>
        </tr>
        <tr>
            <td>UP Health System Portage</td>
            <td>Hancock</td>
            <td>MI</td>
            <td>2149.0</td>
        </tr>
        <tr>
            <td>Main Line Health- Riddle Memorial Hospital</td>
            <td>Media</td>
            <td>PA</td>
            <td>2150.0</td>
        </tr>
        <tr>
            <td>Pelham Medical Center</td>
            <td>Greer</td>
            <td>SC</td>
            <td>2151.0</td>
        </tr>
        <tr>
            <td>Sacred Heart Hospital On the Emerald Coast</td>
            <td>Miramar Beach</td>
            <td>FL</td>
            <td>2152.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Northwest Arkansas</td>
            <td>Rogers</td>
            <td>AR</td>
            <td>2153.0</td>
        </tr>
        <tr>
            <td>AdventHealth New Smyrna Beach</td>
            <td>New Smyrna Beach</td>
            <td>FL</td>
            <td>2154.0</td>
        </tr>
        <tr>
            <td>Aurora Medical Center Oshkosh</td>
            <td>Oshkosh</td>
            <td>WI</td>
            <td>2155.0</td>
        </tr>
        <tr>
            <td>Reston Hospital Center</td>
            <td>Reston</td>
            <td>VA</td>
            <td>2156.0</td>
        </tr>
        <tr>
            <td>Houston Methodist Hospital</td>
            <td>Houston</td>
            <td>TX</td>
            <td>2157.0</td>
        </tr>
        <tr>
            <td>Baptist Beaumont Hospital</td>
            <td>Beaumont</td>
            <td>TX</td>
            <td>2158.0</td>
        </tr>
        <tr>
            <td>HSHS St. Elizabeth&#x27;s Hospital</td>
            <td>O Fallon</td>
            <td>IL</td>
            <td>2159.0</td>
        </tr>
        <tr>
            <td>Texas Health Presbyterian Hospital Plano</td>
            <td>Plano</td>
            <td>TX</td>
            <td>2160.0</td>
        </tr>
        <tr>
            <td>Island Hospital</td>
            <td>Anacortes</td>
            <td>WA</td>
            <td>2161.0</td>
        </tr>
        <tr>
            <td>Genesis Medical Center-Davenport</td>
            <td>Davenport</td>
            <td>IA</td>
            <td>2162.0</td>
        </tr>
        <tr>
            <td>Dixie Regional Medical Center</td>
            <td>St. George</td>
            <td>UT</td>
            <td>2163.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital Sweetwater County</td>
            <td>Rock Springs</td>
            <td>WY</td>
            <td>2164.0</td>
        </tr>
        <tr>
            <td>Memorial Hermann Katy Hospital</td>
            <td>Katy</td>
            <td>TX</td>
            <td>2165.0</td>
        </tr>
        <tr>
            <td>Dupont Hospital</td>
            <td>Fort Wayne</td>
            <td>IN</td>
            <td>2166.0</td>
        </tr>
        <tr>
            <td>East Alabama Medical Center</td>
            <td>Opelika</td>
            <td>AL</td>
            <td>2167.0</td>
        </tr>
        <tr>
            <td>Aurora Lakeland Medical Center</td>
            <td>Elkhorn</td>
            <td>WI</td>
            <td>2168.0</td>
        </tr>
        <tr>
            <td>AdventHealth Ocala</td>
            <td>Ocala</td>
            <td>FL</td>
            <td>2169.0</td>
        </tr>
        <tr>
            <td>Aurora Medical Center Kenosha</td>
            <td>Kenosha</td>
            <td>WI</td>
            <td>2170.0</td>
        </tr>
        <tr>
            <td>St. Jude Medical Center</td>
            <td>Fullerton</td>
            <td>CA</td>
            <td>2171.0</td>
        </tr>
        <tr>
            <td>Houston Methodist The Woodlands Hospital</td>
            <td>The Woodlands</td>
            <td>TX</td>
            <td>2172.0</td>
        </tr>
        <tr>
            <td>Ascension St. Vincent&#x27;s Southside</td>
            <td>Jacksonville</td>
            <td>FL</td>
            <td>2173.0</td>
        </tr>
        <tr>
            <td>Western Missouri Medical Center</td>
            <td>Warrensburg</td>
            <td>MO</td>
            <td>2174.0</td>
        </tr>
        <tr>
            <td>Abrazo Scottsdale Campus</td>
            <td>Phoenix</td>
            <td>AZ</td>
            <td>2175.0</td>
        </tr>
        <tr>
            <td>Baylor Scott &amp; White Medical Center- Waxahachie</td>
            <td>Waxahachie</td>
            <td>TX</td>
            <td>2176.0</td>
        </tr>
        <tr>
            <td>Riverview Medical Center</td>
            <td>Red Bank</td>
            <td>NJ</td>
            <td>2177.0</td>
        </tr>
        <tr>
            <td>Northern Westchester Hospital</td>
            <td>Mount Kisco</td>
            <td>NY</td>
            <td>2178.0</td>
        </tr>
        <tr>
            <td>Aurora Sheboygan Memorial Medical Ctr.</td>
            <td>Sheboygan</td>
            <td>WI</td>
            <td>2179.0</td>
        </tr>
        <tr>
            <td>Southern Tennessee Regional Health System Pulaski</td>
            <td>Pulaski</td>
            <td>TN</td>
            <td>2180.0</td>
        </tr>
        <tr>
            <td>Novant Health Huntersville Medical Center</td>
            <td>Huntersville</td>
            <td>NC</td>
            <td>2181.0</td>
        </tr>
        <tr>
            <td>Forbes Hospital</td>
            <td>Monroeville</td>
            <td>PA</td>
            <td>2182.0</td>
        </tr>
        <tr>
            <td>Henry Ford Wyandotte Hospital</td>
            <td>Wyandotte</td>
            <td>MI</td>
            <td>2183.0</td>
        </tr>
        <tr>
            <td>Trumbull Regional Medical Center</td>
            <td>Warren</td>
            <td>OH</td>
            <td>2184.0</td>
        </tr>
        <tr>
            <td>Lake Granbury Medical Center</td>
            <td>Granbury</td>
            <td>TX</td>
            <td>2185.0</td>
        </tr>
        <tr>
            <td>Woodland Heights Medical Center</td>
            <td>Lufkin</td>
            <td>TX</td>
            <td>2186.0</td>
        </tr>
        <tr>
            <td>Viera Hospital</td>
            <td>Melbourne</td>
            <td>FL</td>
            <td>2187.0</td>
        </tr>
        <tr>
            <td>Adventist La Grange Memorial Hospital</td>
            <td>La Grange</td>
            <td>IL</td>
            <td>2188.0</td>
        </tr>
        <tr>
            <td>Chilton Medical Center</td>
            <td>Pompton Plains</td>
            <td>NJ</td>
            <td>2189.0</td>
        </tr>
        <tr>
            <td>AdventHealth Wesley Chapel</td>
            <td>Wesley Chapel</td>
            <td>FL</td>
            <td>2190.0</td>
        </tr>
        <tr>
            <td>Ascension Crittenton Hospital</td>
            <td>Rochester</td>
            <td>MI</td>
            <td>2192.0</td>
        </tr>
        <tr>
            <td>Delray Medical Center</td>
            <td>Delray Beach</td>
            <td>FL</td>
            <td>2193.0</td>
        </tr>
        <tr>
            <td>Main Line Health- Bryn Mawr Hospital</td>
            <td>Bryn Mawr</td>
            <td>PA</td>
            <td>2194.0</td>
        </tr>
        <tr>
            <td>Palos Community Hospital</td>
            <td>Palos Heights</td>
            <td>IL</td>
            <td>2195.0</td>
        </tr>
        <tr>
            <td>Cleveland Clinic Hospital</td>
            <td>Weston</td>
            <td>FL</td>
            <td>2196.0</td>
        </tr>
        <tr>
            <td>Bethesda Hospital East</td>
            <td>Boynton Beach</td>
            <td>FL</td>
            <td>2197.0</td>
        </tr>
        <tr>
            <td>Hackensack Meridian Health Pascack Valley Medical</td>
            <td>Westwood</td>
            <td>NJ</td>
            <td>2198.0</td>
        </tr>
        <tr>
            <td>Boca Raton Regional Hospital</td>
            <td>Boca Raton</td>
            <td>FL</td>
            <td>2199.0</td>
        </tr>
        <tr>
            <td>HSHS St. Clare Memorial Hospital</td>
            <td>Oconto Falls</td>
            <td>WI</td>
            <td>2200.0</td>
        </tr>
        <tr>
            <td>Heritage Valley Beaver</td>
            <td>Beaver</td>
            <td>PA</td>
            <td>2201.0</td>
        </tr>
        <tr>
            <td>Munson Healthcare Manistee Hospital</td>
            <td>Manistee</td>
            <td>MI</td>
            <td>2202.0</td>
        </tr>
        <tr>
            <td>Gritman Medical Center</td>
            <td>Moscow</td>
            <td>ID</td>
            <td>2203.0</td>
        </tr>
        <tr>
            <td>Steele Memorial Medical Center</td>
            <td>Salmon</td>
            <td>ID</td>
            <td>2204.0</td>
        </tr>
        <tr>
            <td>Watertown Regional Medical Center</td>
            <td>Watertown</td>
            <td>WI</td>
            <td>2205.0</td>
        </tr>
        <tr>
            <td>Franciscan Health Crawfordsville</td>
            <td>Crawfordsville</td>
            <td>IN</td>
            <td>2206.0</td>
        </tr>
        <tr>
            <td>SSM Health Saint Joseph Hospital-Lake Saint Louis</td>
            <td>Lake Saint Louis</td>
            <td>MO</td>
            <td>2207.0</td>
        </tr>
        <tr>
            <td>Cuyuna Regional Medical Center</td>
            <td>Crosby</td>
            <td>MN</td>
            <td>2208.0</td>
        </tr>
        <tr>
            <td>Saint Thomas West Hospital</td>
            <td>Nashville</td>
            <td>TN</td>
            <td>2209.0</td>
        </tr>
        <tr>
            <td>Pipestone CountyÂ¬â€  Medical Center</td>
            <td>Pipestone</td>
            <td>MN</td>
            <td>2210.0</td>
        </tr>
        <tr>
            <td>Wayne County Hospital</td>
            <td>Corydon</td>
            <td>IA</td>
            <td>2211.0</td>
        </tr>
        <tr>
            <td>Indiana University Health Bedford Hospital</td>
            <td>Bedford</td>
            <td>IN</td>
            <td>2212.0</td>
        </tr>
        <tr>
            <td>St. Mary&#x27;s Good Samaritan Hospital</td>
            <td>Greensboro</td>
            <td>GA</td>
            <td>2213.0</td>
        </tr>
        <tr>
            <td>University Hospitals Samaritan Medical Center</td>
            <td>Ashland</td>
            <td>OH</td>
            <td>2214.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Hospital-Gnaden Huetten Campus</td>
            <td>Lehighton</td>
            <td>PA</td>
            <td>2215.0</td>
        </tr>
        <tr>
            <td>Firelands Regional Medical Center</td>
            <td>Sandusky</td>
            <td>OH</td>
            <td>2216.0</td>
        </tr>
        <tr>
            <td>Tennova Healthcare-Harton</td>
            <td>Tullahoma</td>
            <td>TN</td>
            <td>2217.0</td>
        </tr>
        <tr>
            <td>Aspirus Riverview Hospital &amp; Clinics</td>
            <td>Wisconsin Rapids</td>
            <td>WI</td>
            <td>2218.0</td>
        </tr>
        <tr>
            <td>Hendricks Regional Health</td>
            <td>Danville</td>
            <td>IN</td>
            <td>2219.0</td>
        </tr>
        <tr>
            <td>Mercer County Joint Township Community Hospital</td>
            <td>Coldwater</td>
            <td>OH</td>
            <td>2220.0</td>
        </tr>
        <tr>
            <td>Stillwater Medical Center</td>
            <td>Stillwater</td>
            <td>OK</td>
            <td>2221.0</td>
        </tr>
        <tr>
            <td>Saint Thomas Rutherford Hospital</td>
            <td>Murfreesboro</td>
            <td>TN</td>
            <td>2222.0</td>
        </tr>
        <tr>
            <td>Smyth County Community Hospital</td>
            <td>Marion</td>
            <td>VA</td>
            <td>2223.0</td>
        </tr>
        <tr>
            <td>University of Kansas Hlth System St. Francis Campus</td>
            <td>Topeka</td>
            <td>KS</td>
            <td>2224.0</td>
        </tr>
        <tr>
            <td>Brigham and Women&#x27;s Hospital</td>
            <td>Boston</td>
            <td>MA</td>
            <td>2225.0</td>
        </tr>
        <tr>
            <td>Inspira Medical Center Elmer</td>
            <td>Elmer</td>
            <td>NJ</td>
            <td>2226.0</td>
        </tr>
        <tr>
            <td>Charles A. Cannon Jr. Memorial Hospital</td>
            <td>Linville</td>
            <td>NC</td>
            <td>2227.0</td>
        </tr>
        <tr>
            <td>AnMed Health</td>
            <td>Anderson</td>
            <td>SC</td>
            <td>2228.0</td>
        </tr>
        <tr>
            <td>Mercy Walworth Hospital &amp; Medical Center</td>
            <td>Lake Geneva</td>
            <td>WI</td>
            <td>2229.0</td>
        </tr>
        <tr>
            <td>Lansdale Hospital</td>
            <td>Lansdale</td>
            <td>PA</td>
            <td>2230.0</td>
        </tr>
        <tr>
            <td>Bryan Medical Center</td>
            <td>Lincoln</td>
            <td>NE</td>
            <td>2231.0</td>
        </tr>
        <tr>
            <td>Norton Community Hospital</td>
            <td>Norton</td>
            <td>VA</td>
            <td>2232.0</td>
        </tr>
        <tr>
            <td>St. Petersburg General Hospital</td>
            <td>Saint Petersburg</td>
            <td>FL</td>
            <td>2233.0</td>
        </tr>
        <tr>
            <td>Monongahela Valley Hospital</td>
            <td>Monongahela</td>
            <td>PA</td>
            <td>2234.0</td>
        </tr>
        <tr>
            <td>Spectrum Health Ludington Hospital</td>
            <td>Ludington</td>
            <td>MI</td>
            <td>2235.0</td>
        </tr>
        <tr>
            <td>St. Marks Medical Center</td>
            <td>La Grange</td>
            <td>TX</td>
            <td>2236.0</td>
        </tr>
        <tr>
            <td>CHI Oakes Hospital</td>
            <td>Oakes</td>
            <td>ND</td>
            <td>2237.0</td>
        </tr>
        <tr>
            <td>St. Michael&#x27;s Hospital - Cah</td>
            <td>Tyndall</td>
            <td>SD</td>
            <td>2238.0</td>
        </tr>
        <tr>
            <td>Marietta Memorial Hospital</td>
            <td>Marietta</td>
            <td>OH</td>
            <td>2239.0</td>
        </tr>
        <tr>
            <td>Cox Barton County Hospital</td>
            <td>Lamar</td>
            <td>MO</td>
            <td>2240.0</td>
        </tr>
        <tr>
            <td>Greater Regional Medical Center</td>
            <td>Creston</td>
            <td>IA</td>
            <td>2242.0</td>
        </tr>
        <tr>
            <td>St. James Parish Hospital</td>
            <td>Lutcher</td>
            <td>LA</td>
            <td>2243.0</td>
        </tr>
        <tr>
            <td>Hammond Henry Hospital</td>
            <td>Geneseo</td>
            <td>IL</td>
            <td>2244.0</td>
        </tr>
        <tr>
            <td>Meadville Medical Center</td>
            <td>Meadville</td>
            <td>PA</td>
            <td>2245.0</td>
        </tr>
        <tr>
            <td>Ascension Borgess Lee Hospital</td>
            <td>Dowagiac</td>
            <td>MI</td>
            <td>2246.0</td>
        </tr>
        <tr>
            <td>Vidant DuplinÂ¬â€ Hospital</td>
            <td>Kenansville</td>
            <td>NC</td>
            <td>2247.0</td>
        </tr>
        <tr>
            <td>UPMC Altoona</td>
            <td>Altoona</td>
            <td>PA</td>
            <td>2248.0</td>
        </tr>
        <tr>
            <td>Sequoia Hospital</td>
            <td>Redwood City</td>
            <td>CA</td>
            <td>2249.0</td>
        </tr>
        <tr>
            <td>MidMichigan Medical Center - West Branch</td>
            <td>West Branch</td>
            <td>MI</td>
            <td>2250.0</td>
        </tr>
        <tr>
            <td>Unitypoint Health-Marshalltown</td>
            <td>Marshalltown</td>
            <td>IA</td>
            <td>2251.0</td>
        </tr>
        <tr>
            <td>Baptist Health Corbin</td>
            <td>Corbin</td>
            <td>KY</td>
            <td>2252.0</td>
        </tr>
        <tr>
            <td>Robert Wood Johnson University Hospital at Rahway</td>
            <td>Rahway</td>
            <td>NJ</td>
            <td>2253.0</td>
        </tr>
        <tr>
            <td>Memorial Healthcare</td>
            <td>Owosso</td>
            <td>MI</td>
            <td>2254.0</td>
        </tr>
        <tr>
            <td>Fulton County Health Center</td>
            <td>Wauseon</td>
            <td>OH</td>
            <td>2255.0</td>
        </tr>
        <tr>
            <td>Texas Health Harris Methodist Fort Worth</td>
            <td>Fort Worth</td>
            <td>TX</td>
            <td>2256.0</td>
        </tr>
        <tr>
            <td>St. Charles Parish Hospital</td>
            <td>Luling</td>
            <td>LA</td>
            <td>2257.0</td>
        </tr>
        <tr>
            <td>Oak Hill Hospital</td>
            <td>Brooksville</td>
            <td>FL</td>
            <td>2258.0</td>
        </tr>
        <tr>
            <td>Medical City Dallas</td>
            <td>Dallas</td>
            <td>TX</td>
            <td>2259.0</td>
        </tr>
        <tr>
            <td>Floyd Medical Center</td>
            <td>Rome</td>
            <td>GA</td>
            <td>2260.0</td>
        </tr>
        <tr>
            <td>Kittitas Valley Community Hospital</td>
            <td>Ellensburg</td>
            <td>WA</td>
            <td>2261.0</td>
        </tr>
        <tr>
            <td>Aspirus Langlade Hospital</td>
            <td>Antigo</td>
            <td>WI</td>
            <td>2262.0</td>
        </tr>
        <tr>
            <td>Parkview Huntington Hospital</td>
            <td>Huntington</td>
            <td>IN</td>
            <td>2263.0</td>
        </tr>
        <tr>
            <td>Clinton Memorial Hospital</td>
            <td>Wilmington</td>
            <td>OH</td>
            <td>2264.0</td>
        </tr>
        <tr>
            <td>Williamsport Regional Medical Center</td>
            <td>Williamsport</td>
            <td>PA</td>
            <td>2265.0</td>
        </tr>
        <tr>
            <td>UPMC Hamot</td>
            <td>Erie</td>
            <td>PA</td>
            <td>2266.0</td>
        </tr>
        <tr>
            <td>Banner Thunderbird Medical Center</td>
            <td>Glendale</td>
            <td>AZ</td>
            <td>2267.0</td>
        </tr>
        <tr>
            <td>Thedacare Regional Medical Center - Neenah</td>
            <td>Neenah</td>
            <td>WI</td>
            <td>2268.0</td>
        </tr>
        <tr>
            <td>Avera Hand County Memorial Hospital and Clinic</td>
            <td>Miller</td>
            <td>SD</td>
            <td>2269.0</td>
        </tr>
        <tr>
            <td>CHI St. Vincent Morrilton</td>
            <td>Morrilton</td>
            <td>AR</td>
            <td>2270.0</td>
        </tr>
        <tr>
            <td>Riverside Walter Reed Hospital</td>
            <td>Gloucester</td>
            <td>VA</td>
            <td>2271.0</td>
        </tr>
        <tr>
            <td>KershawHealth</td>
            <td>Camden</td>
            <td>SC</td>
            <td>2272.0</td>
        </tr>
        <tr>
            <td>Sisters of Charity Hospital</td>
            <td>Buffalo</td>
            <td>NY</td>
            <td>2273.0</td>
        </tr>
        <tr>
            <td>Robert Packer Hospital</td>
            <td>Sayre</td>
            <td>PA</td>
            <td>2274.0</td>
        </tr>
        <tr>
            <td>St. John&#x27;s Hospital</td>
            <td>Springfield</td>
            <td>IL</td>
            <td>2275.0</td>
        </tr>
        <tr>
            <td>St. Elizabeth Ft. Thomas</td>
            <td>Fort Thomas</td>
            <td>KY</td>
            <td>2276.0</td>
        </tr>
        <tr>
            <td>Community Hospital North</td>
            <td>Indianapolis</td>
            <td>IN</td>
            <td>2277.0</td>
        </tr>
        <tr>
            <td>Providence Hospital</td>
            <td>Mobile</td>
            <td>AL</td>
            <td>2278.0</td>
        </tr>
        <tr>
            <td>St. Josephs Community Hospital of West Bend</td>
            <td>West Bend</td>
            <td>WI</td>
            <td>2280.0</td>
        </tr>
        <tr>
            <td>Portneuf Medical Center</td>
            <td>Pocatello</td>
            <td>ID</td>
            <td>2281.0</td>
        </tr>
        <tr>
            <td>Van Diest Medical Center</td>
            <td>Webster City</td>
            <td>IA</td>
            <td>2282.0</td>
        </tr>
        <tr>
            <td>Terre Haute Regional Hospital</td>
            <td>Terre Haute</td>
            <td>IN</td>
            <td>2283.0</td>
        </tr>
        <tr>
            <td>Hunt Regional Medical Center</td>
            <td>Greenville</td>
            <td>TX</td>
            <td>2284.0</td>
        </tr>
        <tr>
            <td>Vidant Roanoke Chowan Hospital</td>
            <td>Ahoskie</td>
            <td>NC</td>
            <td>2285.0</td>
        </tr>
        <tr>
            <td>Lawrence Memorial Hospital</td>
            <td>Lawrence</td>
            <td>KS</td>
            <td>2286.0</td>
        </tr>
        <tr>
            <td>Texas Health Presbyterian Hospital Allen</td>
            <td>Allen</td>
            <td>TX</td>
            <td>2287.0</td>
        </tr>
        <tr>
            <td>Brandon Regional Hospital</td>
            <td>Brandon</td>
            <td>FL</td>
            <td>2288.0</td>
        </tr>
        <tr>
            <td>University Medical Center-Mesabi/ Mesaba Clinics</td>
            <td>Hibbing</td>
            <td>MN</td>
            <td>2289.0</td>
        </tr>
        <tr>
            <td>Robert Wood Johnson University Hospital Hamilton</td>
            <td>Hamilton</td>
            <td>NJ</td>
            <td>2290.0</td>
        </tr>
        <tr>
            <td>Capital Health Medical Center - Hopewell</td>
            <td>Pennington</td>
            <td>NJ</td>
            <td>2291.0</td>
        </tr>
        <tr>
            <td>Capital Medical Center</td>
            <td>Olympia</td>
            <td>WA</td>
            <td>2292.0</td>
        </tr>
        <tr>
            <td>St. Marys Regional Medical Center</td>
            <td>Russellville</td>
            <td>AR</td>
            <td>2293.0</td>
        </tr>
        <tr>
            <td>Fisher-Titus Hospital</td>
            <td>Norwalk</td>
            <td>OH</td>
            <td>2294.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Joplin</td>
            <td>Joplin</td>
            <td>MO</td>
            <td>2295.0</td>
        </tr>
        <tr>
            <td>Baptist Health Medical Center North Little Rock</td>
            <td>North Little Rock</td>
            <td>AR</td>
            <td>2296.0</td>
        </tr>
        <tr>
            <td>Ocala Regional Medical Center</td>
            <td>Ocala</td>
            <td>FL</td>
            <td>2298.0</td>
        </tr>
        <tr>
            <td>Calverthealth Medical Center</td>
            <td>Prince Frederick</td>
            <td>MD</td>
            <td>2299.0</td>
        </tr>
        <tr>
            <td>MemorialCare Orange Coast Medical Center</td>
            <td>Fountain Valley</td>
            <td>CA</td>
            <td>2300.0</td>
        </tr>
        <tr>
            <td>Haywood Regional Medical Center</td>
            <td>Clyde</td>
            <td>NC</td>
            <td>2301.0</td>
        </tr>
        <tr>
            <td>Tennova Healthcare-Shelbyville</td>
            <td>Shelbyville</td>
            <td>TN</td>
            <td>2302.0</td>
        </tr>
        <tr>
            <td>Penn Highlands Elk</td>
            <td>Saint Marys</td>
            <td>PA</td>
            <td>2303.0</td>
        </tr>
        <tr>
            <td>Ransom Memorial Hospital</td>
            <td>Ottawa</td>
            <td>KS</td>
            <td>2304.0</td>
        </tr>
        <tr>
            <td>Brattleboro Memorial Hospital</td>
            <td>Brattleboro</td>
            <td>VT</td>
            <td>2305.0</td>
        </tr>
        <tr>
            <td>Beaver Dam Community Hospital</td>
            <td>Beaver Dam</td>
            <td>WI</td>
            <td>2306.0</td>
        </tr>
        <tr>
            <td>Baptist Medical Center Jacksonville</td>
            <td>Jacksonville</td>
            <td>FL</td>
            <td>2307.0</td>
        </tr>
        <tr>
            <td>Fort Walton Beach Medical Center</td>
            <td>Fort Walton Beach</td>
            <td>FL</td>
            <td>2308.0</td>
        </tr>
        <tr>
            <td>Lenox Hill Hospital</td>
            <td>New York</td>
            <td>NY</td>
            <td>2309.0</td>
        </tr>
        <tr>
            <td>Delaware County Memorial Hospital</td>
            <td>Drexel Hill</td>
            <td>PA</td>
            <td>2310.0</td>
        </tr>
        <tr>
            <td>Munson Healthcare Otsego Memorial Hospital</td>
            <td>Gaylord</td>
            <td>MI</td>
            <td>2311.0</td>
        </tr>
        <tr>
            <td>San Antonio Regional Hospital</td>
            <td>Upland</td>
            <td>CA</td>
            <td>2312.0</td>
        </tr>
        <tr>
            <td>St. Anthonys Memorial Hospital</td>
            <td>Effingham</td>
            <td>IL</td>
            <td>2313.0</td>
        </tr>
        <tr>
            <td>Aurora West Allis Medical Center</td>
            <td>West Allis</td>
            <td>WI</td>
            <td>2314.0</td>
        </tr>
        <tr>
            <td>Saint John Hospital</td>
            <td>Leavenworth</td>
            <td>KS</td>
            <td>2315.0</td>
        </tr>
        <tr>
            <td>Little Company of Mary Hospital</td>
            <td>Evergreen Park</td>
            <td>IL</td>
            <td>2316.0</td>
        </tr>
        <tr>
            <td>St. Vincent Medical Center/North</td>
            <td>Sherwood</td>
            <td>AR</td>
            <td>2317.0</td>
        </tr>
        <tr>
            <td>OhioHealth Mansfield Hospital</td>
            <td>Mansfield</td>
            <td>OH</td>
            <td>2318.0</td>
        </tr>
        <tr>
            <td>Singing River Gulfport</td>
            <td>Gulfport</td>
            <td>MS</td>
            <td>2319.0</td>
        </tr>
        <tr>
            <td>Proctor Hospital</td>
            <td>Peoria</td>
            <td>IL</td>
            <td>2320.0</td>
        </tr>
        <tr>
            <td>UT Health East Texas Athens Hospital</td>
            <td>Athens</td>
            <td>TX</td>
            <td>2321.0</td>
        </tr>
        <tr>
            <td>Chandler Regional Medical Center</td>
            <td>Chandler</td>
            <td>AZ</td>
            <td>2322.0</td>
        </tr>
        <tr>
            <td>Highlands Cashiers Hospital</td>
            <td>Highlands</td>
            <td>NC</td>
            <td>2323.0</td>
        </tr>
        <tr>
            <td>Washakie Medical Center</td>
            <td>Worland</td>
            <td>WY</td>
            <td>2324.0</td>
        </tr>
        <tr>
            <td>Hackettstown Medical Center</td>
            <td>Hackettstown</td>
            <td>NJ</td>
            <td>2325.0</td>
        </tr>
        <tr>
            <td>Margaret Mary Health</td>
            <td>Batesville</td>
            <td>IN</td>
            <td>2326.0</td>
        </tr>
        <tr>
            <td>Olathe Medical Center</td>
            <td>Olathe</td>
            <td>KS</td>
            <td>2327.0</td>
        </tr>
        <tr>
            <td>Allegheny General Hospital</td>
            <td>Pittsburgh</td>
            <td>PA</td>
            <td>2328.0</td>
        </tr>
        <tr>
            <td>Beaumont Hospital, Troy</td>
            <td>Troy</td>
            <td>MI</td>
            <td>2329.0</td>
        </tr>
        <tr>
            <td>Major Hospital</td>
            <td>Shelbyville</td>
            <td>IN</td>
            <td>2330.0</td>
        </tr>
        <tr>
            <td>Jones Regional Medical Center</td>
            <td>Anamosa</td>
            <td>IA</td>
            <td>2331.0</td>
        </tr>
        <tr>
            <td>Saint Luke&#x27;s South Hospital</td>
            <td>Overland Park</td>
            <td>KS</td>
            <td>2332.0</td>
        </tr>
        <tr>
            <td>Wilson Memorial Hospital</td>
            <td>Sidney</td>
            <td>OH</td>
            <td>2333.0</td>
        </tr>
        <tr>
            <td>Medical West, An Affiliate of UAB Health System</td>
            <td>Bessemer</td>
            <td>AL</td>
            <td>2334.0</td>
        </tr>
        <tr>
            <td>Medical Center of South Arkansas</td>
            <td>El Dorado</td>
            <td>AR</td>
            <td>2335.0</td>
        </tr>
        <tr>
            <td>Monongalia County General Hospital</td>
            <td>Morgantown</td>
            <td>WV</td>
            <td>2336.0</td>
        </tr>
        <tr>
            <td>Southern Tennessee Regional Health System Lawrence</td>
            <td>Lawrenceburg</td>
            <td>TN</td>
            <td>2337.0</td>
        </tr>
        <tr>
            <td>Canonsburg General Hospital</td>
            <td>Canonsburg</td>
            <td>PA</td>
            <td>2338.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Kingfisher</td>
            <td>Kingfisher</td>
            <td>OK</td>
            <td>2339.0</td>
        </tr>
        <tr>
            <td>Northern Hospital of Surry County</td>
            <td>Mount Airy</td>
            <td>NC</td>
            <td>2340.0</td>
        </tr>
        <tr>
            <td>Davis Hospital and Medical Center</td>
            <td>Layton</td>
            <td>UT</td>
            <td>2341.0</td>
        </tr>
        <tr>
            <td>Ocean Medical Center</td>
            <td>Brick</td>
            <td>NJ</td>
            <td>2342.0</td>
        </tr>
        <tr>
            <td>Victor Valley Global Medical Center</td>
            <td>Victorville</td>
            <td>CA</td>
            <td>2343.0</td>
        </tr>
        <tr>
            <td>Tidelands Waccamaw Community Hospital</td>
            <td>Murrells Inlet</td>
            <td>SC</td>
            <td>2344.0</td>
        </tr>
        <tr>
            <td>St. Joseph&#x27;s Medical Center of Stockton</td>
            <td>Stockton</td>
            <td>CA</td>
            <td>2345.0</td>
        </tr>
        <tr>
            <td>Greenbrier Valley Medical Center</td>
            <td>Ronceverte</td>
            <td>WV</td>
            <td>2346.0</td>
        </tr>
        <tr>
            <td>Saint Lukes North Hospital</td>
            <td>Kansas City</td>
            <td>MO</td>
            <td>2347.0</td>
        </tr>
        <tr>
            <td>Newman Regional Health</td>
            <td>Emporia</td>
            <td>KS</td>
            <td>2348.0</td>
        </tr>
        <tr>
            <td>Syracuse Area Health</td>
            <td>Syracuse</td>
            <td>NE</td>
            <td>2349.0</td>
        </tr>
        <tr>
            <td>Hamilton Medical Center</td>
            <td>Dalton</td>
            <td>GA</td>
            <td>2350.0</td>
        </tr>
        <tr>
            <td>Jefferson Medical Center</td>
            <td>Ranson</td>
            <td>WV</td>
            <td>2351.0</td>
        </tr>
        <tr>
            <td>Tishomingo Health Services</td>
            <td>Iuka</td>
            <td>MS</td>
            <td>2352.0</td>
        </tr>
        <tr>
            <td>Loma Linda University Medical Center-Murrieta</td>
            <td>Murrieta</td>
            <td>CA</td>
            <td>2353.0</td>
        </tr>
        <tr>
            <td>Good Samaritan Hospital of Suffern</td>
            <td>Suffern</td>
            <td>NY</td>
            <td>2354.0</td>
        </tr>
        <tr>
            <td>Southeast Alabama Medical Center</td>
            <td>Dothan</td>
            <td>AL</td>
            <td>2355.0</td>
        </tr>
        <tr>
            <td>Abraham Lincoln Memorial Hospital</td>
            <td>Lincoln</td>
            <td>IL</td>
            <td>2356.0</td>
        </tr>
        <tr>
            <td>McDonough District Hospital</td>
            <td>Macomb</td>
            <td>IL</td>
            <td>2357.0</td>
        </tr>
        <tr>
            <td>PIH Hospital - Downey</td>
            <td>Downey</td>
            <td>CA</td>
            <td>2358.0</td>
        </tr>
        <tr>
            <td>Carolina East Medical Center</td>
            <td>New Bern</td>
            <td>NC</td>
            <td>2359.0</td>
        </tr>
        <tr>
            <td>Western Plains Medical Complex</td>
            <td>Dodge City</td>
            <td>KS</td>
            <td>2360.0</td>
        </tr>
        <tr>
            <td>Wayne Hospital</td>
            <td>Greenville</td>
            <td>OH</td>
            <td>2361.0</td>
        </tr>
        <tr>
            <td>Valley Regional Medical Center</td>
            <td>Brownsville</td>
            <td>TX</td>
            <td>2362.0</td>
        </tr>
        <tr>
            <td>Rapides Regional Medical Center</td>
            <td>Alexandria</td>
            <td>LA</td>
            <td>2363.0</td>
        </tr>
        <tr>
            <td>Rockville General Hospital</td>
            <td>Rockville</td>
            <td>CT</td>
            <td>2364.0</td>
        </tr>
        <tr>
            <td>Parkland Medical Center</td>
            <td>Derry</td>
            <td>NH</td>
            <td>2365.0</td>
        </tr>
        <tr>
            <td>Providence Tarzana Medical Center</td>
            <td>Tarzana</td>
            <td>CA</td>
            <td>2366.0</td>
        </tr>
        <tr>
            <td>Abrazo Arrowhead Campus</td>
            <td>Glendale</td>
            <td>AZ</td>
            <td>2367.0</td>
        </tr>
        <tr>
            <td>San Gabriel Valley Medical Center</td>
            <td>San Gabriel</td>
            <td>CA</td>
            <td>2368.0</td>
        </tr>
        <tr>
            <td>Day Kimball Hospital</td>
            <td>Putnam</td>
            <td>CT</td>
            <td>2369.0</td>
        </tr>
        <tr>
            <td>Mercyone Centerville Medical Center</td>
            <td>Centerville</td>
            <td>IA</td>
            <td>2370.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital of Folsom</td>
            <td>Folsom</td>
            <td>CA</td>
            <td>2371.0</td>
        </tr>
        <tr>
            <td>Mobile Infirmary Medical Center</td>
            <td>Mobile</td>
            <td>AL</td>
            <td>2372.0</td>
        </tr>
        <tr>
            <td>Marion Regional Medical Center</td>
            <td>Hamilton</td>
            <td>AL</td>
            <td>2373.0</td>
        </tr>
        <tr>
            <td>Lewisgale Hospital Pulaski</td>
            <td>Pulaski</td>
            <td>VA</td>
            <td>2374.0</td>
        </tr>
        <tr>
            <td>NEA Baptist Memorial Hospital</td>
            <td>Jonesboro</td>
            <td>AR</td>
            <td>2375.0</td>
        </tr>
        <tr>
            <td>Ascension Macomb Oakland Hosp-Warren Campus</td>
            <td>Warren</td>
            <td>MI</td>
            <td>2376.0</td>
        </tr>
        <tr>
            <td>Lakes Regional Healthcare</td>
            <td>Spirit Lake</td>
            <td>IA</td>
            <td>2377.0</td>
        </tr>
        <tr>
            <td>Nor-Lea Hospital District</td>
            <td>Lovington</td>
            <td>NM</td>
            <td>2378.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital of Buffalo</td>
            <td>Buffalo</td>
            <td>NY</td>
            <td>2379.0</td>
        </tr>
        <tr>
            <td>Defiance Regional Medical Center</td>
            <td>Defiance</td>
            <td>OH</td>
            <td>2380.0</td>
        </tr>
        <tr>
            <td>AuburnÂ¬â€  Community Hospital</td>
            <td>Auburn</td>
            <td>NY</td>
            <td>2381.0</td>
        </tr>
        <tr>
            <td>Waukesha Memorial Hospital</td>
            <td>Waukesha</td>
            <td>WI</td>
            <td>2384.0</td>
        </tr>
        <tr>
            <td>Regional Hospital of Scranton</td>
            <td>Scranton</td>
            <td>PA</td>
            <td>2385.0</td>
        </tr>
        <tr>
            <td>AllianceHealth Woodward</td>
            <td>Woodward</td>
            <td>OK</td>
            <td>2386.0</td>
        </tr>
        <tr>
            <td>SSM Health St. Clare Hospital - Fenton</td>
            <td>Fenton</td>
            <td>MO</td>
            <td>2387.0</td>
        </tr>
        <tr>
            <td>Pomona Valley Hospital Medical Center</td>
            <td>Pomona</td>
            <td>CA</td>
            <td>2388.0</td>
        </tr>
        <tr>
            <td>Katherine Shaw Bethea Hospital</td>
            <td>Dixon</td>
            <td>IL</td>
            <td>2389.0</td>
        </tr>
        <tr>
            <td>Hillcrest Hospital South</td>
            <td>Tulsa</td>
            <td>OK</td>
            <td>2390.0</td>
        </tr>
        <tr>
            <td>Harrison County Hospital</td>
            <td>Corydon</td>
            <td>IN</td>
            <td>2391.0</td>
        </tr>
        <tr>
            <td>HSHS Holy Family Hospial</td>
            <td>Greenville</td>
            <td>IL</td>
            <td>2392.0</td>
        </tr>
        <tr>
            <td>Methodist Mansfield Medical Center</td>
            <td>Mansfield</td>
            <td>TX</td>
            <td>2393.0</td>
        </tr>
        <tr>
            <td>Brazosport Regional Health System</td>
            <td>Lake Jackson</td>
            <td>TX</td>
            <td>2394.0</td>
        </tr>
        <tr>
            <td>Red Bud Regional Hospital</td>
            <td>Red Bud</td>
            <td>IL</td>
            <td>2395.0</td>
        </tr>
        <tr>
            <td>Florida Hospital Carrollwood</td>
            <td>Tampa</td>
            <td>FL</td>
            <td>2396.0</td>
        </tr>
        <tr>
            <td>Emanate Health Foothill Presbyterian Hospital</td>
            <td>Glendora</td>
            <td>CA</td>
            <td>2397.0</td>
        </tr>
        <tr>
            <td>Crouse Hospital</td>
            <td>Syracuse</td>
            <td>NY</td>
            <td>2398.0</td>
        </tr>
        <tr>
            <td>Baylor Scott And White Medical Center Sunnyvale</td>
            <td>Sunnyvale</td>
            <td>TX</td>
            <td>2400.0</td>
        </tr>
        <tr>
            <td>Hutchinson Regional Medical Center</td>
            <td>Hutchinson</td>
            <td>KS</td>
            <td>2401.0</td>
        </tr>
        <tr>
            <td>Vidant Beaufort Hospital</td>
            <td>Washington</td>
            <td>NC</td>
            <td>2402.0</td>
        </tr>
        <tr>
            <td>Sampson Regional Medical Center</td>
            <td>Clinton</td>
            <td>NC</td>
            <td>2403.0</td>
        </tr>
        <tr>
            <td>Texas Health Presbyterian Hospital Denton</td>
            <td>Denton</td>
            <td>TX</td>
            <td>2404.0</td>
        </tr>
        <tr>
            <td>CHI Health Midlands</td>
            <td>Papillion</td>
            <td>NE</td>
            <td>2405.0</td>
        </tr>
        <tr>
            <td>Baylor Scott and White Medical Center Lake Pointe</td>
            <td>Rowlett</td>
            <td>TX</td>
            <td>2406.0</td>
        </tr>
        <tr>
            <td>St. James Mercy Hospital</td>
            <td>Hornell</td>
            <td>NY</td>
            <td>2407.0</td>
        </tr>
        <tr>
            <td>Saint Thomas Highlands Hospital</td>
            <td>Sparta</td>
            <td>TN</td>
            <td>2408.0</td>
        </tr>
        <tr>
            <td>Fawcett Memorial Hospital</td>
            <td>Port Charlotte</td>
            <td>FL</td>
            <td>2409.0</td>
        </tr>
        <tr>
            <td>Johnson Memorial Hospital</td>
            <td>Franklin</td>
            <td>IN</td>
            <td>2410.0</td>
        </tr>
        <tr>
            <td>Morris Hospital &amp; Healthcare Centers</td>
            <td>Morris</td>
            <td>IL</td>
            <td>2411.0</td>
        </tr>
        <tr>
            <td>Ascension River District Hospital</td>
            <td>East China</td>
            <td>MI</td>
            <td>2412.0</td>
        </tr>
        <tr>
            <td>JFK Medical Center</td>
            <td>Atlantis</td>
            <td>FL</td>
            <td>2413.0</td>
        </tr>
        <tr>
            <td>Community Hospital South</td>
            <td>Indianapolis</td>
            <td>IN</td>
            <td>2415.0</td>
        </tr>
        <tr>
            <td>Cobre Valley Regional Medical Center</td>
            <td>Globe</td>
            <td>AZ</td>
            <td>2416.0</td>
        </tr>
        <tr>
            <td>AdventHealth Deland</td>
            <td>Deland</td>
            <td>FL</td>
            <td>2417.0</td>
        </tr>
        <tr>
            <td>Buena Vista Regional Medical Center</td>
            <td>Storm Lake</td>
            <td>IA</td>
            <td>2418.0</td>
        </tr>
        <tr>
            <td>Baxter Regional Medical Center</td>
            <td>Mountain Home</td>
            <td>AR</td>
            <td>2419.0</td>
        </tr>
        <tr>
            <td>Sparks Medical Center - Fort Smith</td>
            <td>Fort Smith</td>
            <td>AR</td>
            <td>2420.0</td>
        </tr>
        <tr>
            <td>Phoebe Putney Memorial Hospital</td>
            <td>Albany</td>
            <td>GA</td>
            <td>2421.0</td>
        </tr>
        <tr>
            <td>Jamestown Regional Medical Center</td>
            <td>Jamestown</td>
            <td>ND</td>
            <td>2422.0</td>
        </tr>
        <tr>
            <td>Aurora Medical Center - Grafton</td>
            <td>Grafton</td>
            <td>WI</td>
            <td>2423.0</td>
        </tr>
        <tr>
            <td>Steward Sebastian River Medical Center</td>
            <td>Sebastian</td>
            <td>FL</td>
            <td>2425.0</td>
        </tr>
        <tr>
            <td>Livingston Healthcare</td>
            <td>Livingston</td>
            <td>MT</td>
            <td>2426.0</td>
        </tr>
        <tr>
            <td>Claiborne Medical Center</td>
            <td>Tazewell</td>
            <td>TN</td>
            <td>2427.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital of Carbondale</td>
            <td>Carbondale</td>
            <td>IL</td>
            <td>2428.0</td>
        </tr>
        <tr>
            <td>Beaumont Hospital - Wayne</td>
            <td>Wayne</td>
            <td>MI</td>
            <td>2429.0</td>
        </tr>
        <tr>
            <td>Providence Little Company of Mary Medical Center Torrance</td>
            <td>Torrance</td>
            <td>CA</td>
            <td>2430.0</td>
        </tr>
        <tr>
            <td>Graham Regional Medical Center</td>
            <td>Graham</td>
            <td>TX</td>
            <td>2431.0</td>
        </tr>
        <tr>
            <td>Bothwell Regional Health Center</td>
            <td>Sedalia</td>
            <td>MO</td>
            <td>2432.0</td>
        </tr>
        <tr>
            <td>Methodist Richardson Medical Center</td>
            <td>Richardson</td>
            <td>TX</td>
            <td>2433.0</td>
        </tr>
        <tr>
            <td>VHS Harlingen Hospital Company</td>
            <td>Harlingen</td>
            <td>TX</td>
            <td>2434.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital of Tampa</td>
            <td>Tampa</td>
            <td>FL</td>
            <td>2435.0</td>
        </tr>
        <tr>
            <td>Overland Park Reg Medical Center</td>
            <td>Overland Park</td>
            <td>KS</td>
            <td>2436.0</td>
        </tr>
        <tr>
            <td>Wilson N. Jones Regional Medical Center</td>
            <td>Sherman</td>
            <td>TX</td>
            <td>2437.0</td>
        </tr>
        <tr>
            <td>J. C. Blair Memorial Hospital</td>
            <td>Huntingdon</td>
            <td>PA</td>
            <td>2438.0</td>
        </tr>
        <tr>
            <td>Illini Community Hospital</td>
            <td>Pittsfield</td>
            <td>IL</td>
            <td>2439.0</td>
        </tr>
        <tr>
            <td>Froedtert South - Kenosha Medical Center</td>
            <td>Kenosha</td>
            <td>WI</td>
            <td>2440.0</td>
        </tr>
        <tr>
            <td>Randolph Hospital</td>
            <td>Asheboro</td>
            <td>NC</td>
            <td>2441.0</td>
        </tr>
        <tr>
            <td>Central Carolina Hospital</td>
            <td>Sanford</td>
            <td>NC</td>
            <td>2442.0</td>
        </tr>
        <tr>
            <td>Mountain View Regional Medical Center</td>
            <td>Las Cruces</td>
            <td>NM</td>
            <td>2443.0</td>
        </tr>
        <tr>
            <td>Lake Regional Health System</td>
            <td>Osage Beach</td>
            <td>MO</td>
            <td>2444.0</td>
        </tr>
        <tr>
            <td>Lake Cumberland Regional Hospital</td>
            <td>Somerset</td>
            <td>KY</td>
            <td>2445.0</td>
        </tr>
        <tr>
            <td>North Baldwin Infirmary</td>
            <td>Bay Minette</td>
            <td>AL</td>
            <td>2446.0</td>
        </tr>
        <tr>
            <td>St. John&#x27;s Riverside Hospital</td>
            <td>Yonkers</td>
            <td>NY</td>
            <td>2447.0</td>
        </tr>
        <tr>
            <td>Scotland Memorial Hospital</td>
            <td>Laurinburg</td>
            <td>NC</td>
            <td>2448.0</td>
        </tr>
        <tr>
            <td>Merrick Medical Center</td>
            <td>Central City</td>
            <td>NE</td>
            <td>2449.0</td>
        </tr>
        <tr>
            <td>MH St. Elizabeth Boardman Hospital</td>
            <td>Boardman</td>
            <td>OH</td>
            <td>2450.0</td>
        </tr>
        <tr>
            <td>Northeast Alabama Regional Medical Center</td>
            <td>Anniston</td>
            <td>AL</td>
            <td>2451.0</td>
        </tr>
        <tr>
            <td>Saint Mary&#x27;s Standish Community Hospital</td>
            <td>Standish</td>
            <td>MI</td>
            <td>2452.0</td>
        </tr>
        <tr>
            <td>HCA Houston Healthcare Tomball</td>
            <td>Tomball</td>
            <td>TX</td>
            <td>2453.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital Pembroke</td>
            <td>Pembroke Pines</td>
            <td>FL</td>
            <td>2454.0</td>
        </tr>
        <tr>
            <td>Henry County Memorial Hospital</td>
            <td>New Castle</td>
            <td>IN</td>
            <td>2455.0</td>
        </tr>
        <tr>
            <td>Avera Creighton Hospital</td>
            <td>Creighton</td>
            <td>NE</td>
            <td>2456.0</td>
        </tr>
        <tr>
            <td>Jennersville Hospital</td>
            <td>West Grove</td>
            <td>PA</td>
            <td>2457.0</td>
        </tr>
        <tr>
            <td>Prattville Baptist Hospital</td>
            <td>Prattville</td>
            <td>AL</td>
            <td>2458.0</td>
        </tr>
        <tr>
            <td>Methodist Hospital of Southern CA</td>
            <td>Arcadia</td>
            <td>CA</td>
            <td>2459.0</td>
        </tr>
        <tr>
            <td>Ascension Sacred Heart Hospital</td>
            <td>Tomahawk</td>
            <td>WI</td>
            <td>2460.0</td>
        </tr>
        <tr>
            <td>Palmetto Health Tuomey Hospital</td>
            <td>Sumter</td>
            <td>SC</td>
            <td>2461.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital West</td>
            <td>Pembroke Pines</td>
            <td>FL</td>
            <td>2462.0</td>
        </tr>
        <tr>
            <td>Siloam Springs Regional Hospital</td>
            <td>Siloam Springs</td>
            <td>AR</td>
            <td>2463.0</td>
        </tr>
        <tr>
            <td>St. Joseph Mercy Oakland</td>
            <td>Pontiac</td>
            <td>MI</td>
            <td>2464.0</td>
        </tr>
        <tr>
            <td>Ennis Regional Medical Center</td>
            <td>Ennis</td>
            <td>TX</td>
            <td>2465.0</td>
        </tr>
        <tr>
            <td>Titusville Hospital</td>
            <td>Titusville</td>
            <td>PA</td>
            <td>2466.0</td>
        </tr>
        <tr>
            <td>San Ramon Regional Medical Center</td>
            <td>San Ramon</td>
            <td>CA</td>
            <td>2467.0</td>
        </tr>
        <tr>
            <td>Logan Memorial Hospital</td>
            <td>Russellville</td>
            <td>KY</td>
            <td>2468.0</td>
        </tr>
        <tr>
            <td>Novant Health Brunswick Medical Center</td>
            <td>Supply</td>
            <td>NC</td>
            <td>2469.0</td>
        </tr>
        <tr>
            <td>Berwick Hospital Center</td>
            <td>Berwick</td>
            <td>PA</td>
            <td>2470.0</td>
        </tr>
        <tr>
            <td>Bucyrus Community Hospital</td>
            <td>Bucyrus</td>
            <td>OH</td>
            <td>2471.0</td>
        </tr>
        <tr>
            <td>Phoebe Sumter Medical Center</td>
            <td>Americus</td>
            <td>GA</td>
            <td>2473.0</td>
        </tr>
        <tr>
            <td>Fayette Medical Center</td>
            <td>Fayette</td>
            <td>AL</td>
            <td>2474.0</td>
        </tr>
        <tr>
            <td>UT Health East Texas Jacksonville Hospital</td>
            <td>Jacksonville</td>
            <td>TX</td>
            <td>2475.0</td>
        </tr>
        <tr>
            <td>Ozarks Medical Center</td>
            <td>West Plains</td>
            <td>MO</td>
            <td>2476.0</td>
        </tr>
        <tr>
            <td>Promedica Coldwater Regional Hospital</td>
            <td>Coldwater</td>
            <td>MI</td>
            <td>2477.0</td>
        </tr>
        <tr>
            <td>CHI St. Alexius Health Williston</td>
            <td>Williston</td>
            <td>ND</td>
            <td>2478.0</td>
        </tr>
        <tr>
            <td>Novant Health Rowan Medical Center</td>
            <td>Salisbury</td>
            <td>NC</td>
            <td>2479.0</td>
        </tr>
        <tr>
            <td>Our Lady of Lourdes Regional Medical Center</td>
            <td>Lafayette</td>
            <td>LA</td>
            <td>2480.0</td>
        </tr>
        <tr>
            <td>Franciscan Health Olympia &amp; Chicago Heights</td>
            <td>Olympia Fields</td>
            <td>IL</td>
            <td>2481.0</td>
        </tr>
        <tr>
            <td>Medina Memorial Hospital</td>
            <td>Medina</td>
            <td>NY</td>
            <td>2482.0</td>
        </tr>
        <tr>
            <td>Valley West Community Hospital</td>
            <td>Sandwich</td>
            <td>IL</td>
            <td>2483.0</td>
        </tr>
        <tr>
            <td>Presence Saint Joseph Medical Center</td>
            <td>Joliet</td>
            <td>IL</td>
            <td>2484.0</td>
        </tr>
        <tr>
            <td>Henry County Medical Center</td>
            <td>Paris</td>
            <td>TN</td>
            <td>2485.0</td>
        </tr>
        <tr>
            <td>West Calcasieu Cameron Hospital</td>
            <td>Sulphur</td>
            <td>LA</td>
            <td>2486.0</td>
        </tr>
        <tr>
            <td>Butler Memorial Hospital</td>
            <td>Butler</td>
            <td>PA</td>
            <td>2487.0</td>
        </tr>
        <tr>
            <td>Beverly Hospital</td>
            <td>Montebello</td>
            <td>CA</td>
            <td>2488.0</td>
        </tr>
        <tr>
            <td>Upper Valley Medical Center</td>
            <td>Troy</td>
            <td>OH</td>
            <td>2489.0</td>
        </tr>
        <tr>
            <td>Samaritan Medical Center</td>
            <td>Watertown</td>
            <td>NY</td>
            <td>2490.0</td>
        </tr>
        <tr>
            <td>Mosaic Medical Center â€šÃ„Ã¬ Maryville</td>
            <td>Maryville</td>
            <td>MO</td>
            <td>2491.0</td>
        </tr>
        <tr>
            <td>University of Maryland Balto WashingtonÂ¬â€  Medical Center</td>
            <td>Glen Burnie</td>
            <td>MD</td>
            <td>2492.0</td>
        </tr>
        <tr>
            <td>St. Mary&#x27;s Medical Center</td>
            <td>West Palm Beach</td>
            <td>FL</td>
            <td>2493.0</td>
        </tr>
        <tr>
            <td>Cedars-Sinai Medical Center</td>
            <td>Los Angeles</td>
            <td>CA</td>
            <td>2494.0</td>
        </tr>
        <tr>
            <td>Slidell Memorial Hospital</td>
            <td>Slidell</td>
            <td>LA</td>
            <td>2495.0</td>
        </tr>
        <tr>
            <td>Baptist Health Madisonville</td>
            <td>Madisonville</td>
            <td>KY</td>
            <td>2496.0</td>
        </tr>
        <tr>
            <td>North Alabama Medical Center</td>
            <td>Florence</td>
            <td>AL</td>
            <td>2497.0</td>
        </tr>
        <tr>
            <td>Williamson Medical Center</td>
            <td>Franklin</td>
            <td>TN</td>
            <td>2498.0</td>
        </tr>
        <tr>
            <td>Wetzel County Hospital</td>
            <td>New Martinsville</td>
            <td>WV</td>
            <td>2499.0</td>
        </tr>
        <tr>
            <td>Broward Health Imperial Point</td>
            <td>Fort Lauderdale</td>
            <td>FL</td>
            <td>2500.0</td>
        </tr>
        <tr>
            <td>Sturgis Hospital</td>
            <td>Sturgis</td>
            <td>MI</td>
            <td>2501.0</td>
        </tr>
        <tr>
            <td>Floyd Valley Healthcare</td>
            <td>Le Mars</td>
            <td>IA</td>
            <td>2502.0</td>
        </tr>
        <tr>
            <td>White Plains Hospital Center</td>
            <td>White Plains</td>
            <td>NY</td>
            <td>2503.0</td>
        </tr>
        <tr>
            <td>Heart of Florida Regional Medical Center</td>
            <td>Davenport</td>
            <td>FL</td>
            <td>2504.0</td>
        </tr>
        <tr>
            <td>Hedrick Medical Center</td>
            <td>Chillicothe</td>
            <td>MO</td>
            <td>2505.0</td>
        </tr>
        <tr>
            <td>Evangelical Community Hospital</td>
            <td>Lewisburg</td>
            <td>PA</td>
            <td>2506.0</td>
        </tr>
        <tr>
            <td>Roane General Hospital</td>
            <td>Spencer</td>
            <td>WV</td>
            <td>2507.0</td>
        </tr>
        <tr>
            <td>Cedar-Sinai Marina Del Rey Hospital</td>
            <td>Marina Del Rey</td>
            <td>CA</td>
            <td>2508.0</td>
        </tr>
        <tr>
            <td>William Newton Hospital</td>
            <td>Winfield</td>
            <td>KS</td>
            <td>2509.0</td>
        </tr>
        <tr>
            <td>Mercy Medical Center-Clinton</td>
            <td>Clinton</td>
            <td>IA</td>
            <td>2510.0</td>
        </tr>
        <tr>
            <td>Saint Francis Bartlett Medical Center</td>
            <td>Bartlett</td>
            <td>TN</td>
            <td>2511.0</td>
        </tr>
        <tr>
            <td>Sparrow Carson Hospital</td>
            <td>Carson City</td>
            <td>MI</td>
            <td>2512.0</td>
        </tr>
        <tr>
            <td>Highpoint Health</td>
            <td>Lawrenceburg</td>
            <td>IN</td>
            <td>2513.0</td>
        </tr>
        <tr>
            <td>Howard County Medical Center</td>
            <td>St. Paul</td>
            <td>NE</td>
            <td>2515.0</td>
        </tr>
        <tr>
            <td>Weiser Memorial Hospital</td>
            <td>Weiser</td>
            <td>ID</td>
            <td>2516.0</td>
        </tr>
        <tr>
            <td>Garfield Medical Center</td>
            <td>Monterey Park</td>
            <td>CA</td>
            <td>2517.0</td>
        </tr>
        <tr>
            <td>Carson Tahoe Regional Medical Center</td>
            <td>Carson City</td>
            <td>NV</td>
            <td>2518.0</td>
        </tr>
        <tr>
            <td>Evanston Regional Hospital</td>
            <td>Evanston</td>
            <td>WY</td>
            <td>2519.0</td>
        </tr>
        <tr>
            <td>Sharon Regional Health System</td>
            <td>Sharon</td>
            <td>PA</td>
            <td>2520.0</td>
        </tr>
        <tr>
            <td>Baptist Health Medical Center-Stuttgart</td>
            <td>Stuttgart</td>
            <td>AR</td>
            <td>2521.0</td>
        </tr>
        <tr>
            <td>Crestwood Medical Center</td>
            <td>Huntsville</td>
            <td>AL</td>
            <td>2522.0</td>
        </tr>
        <tr>
            <td>AllianceHealth Clinton</td>
            <td>Clinton</td>
            <td>OK</td>
            <td>2523.0</td>
        </tr>
        <tr>
            <td>UNC Lenoir Health Care</td>
            <td>Kinston</td>
            <td>NC</td>
            <td>2524.0</td>
        </tr>
        <tr>
            <td>Norwood Hospital</td>
            <td>Norwood</td>
            <td>MA</td>
            <td>2526.0</td>
        </tr>
        <tr>
            <td>Jefferson Stratford Hospital</td>
            <td>Stratford</td>
            <td>NJ</td>
            <td>2527.0</td>
        </tr>
        <tr>
            <td>Mesa View Regional Hospital</td>
            <td>Mesquite</td>
            <td>NV</td>
            <td>2528.0</td>
        </tr>
        <tr>
            <td>St. Bernards Medical Center</td>
            <td>Jonesboro</td>
            <td>AR</td>
            <td>2529.0</td>
        </tr>
        <tr>
            <td>Susan B Allen Memorial Hospital</td>
            <td>El Dorado</td>
            <td>KS</td>
            <td>2530.0</td>
        </tr>
        <tr>
            <td>Atchison Hospital</td>
            <td>Atchison</td>
            <td>KS</td>
            <td>2531.0</td>
        </tr>
        <tr>
            <td>Mad River Community Hospital</td>
            <td>Arcata</td>
            <td>CA</td>
            <td>2532.0</td>
        </tr>
        <tr>
            <td>HSHS Good Shepherd Hospital</td>
            <td>Shelbyville</td>
            <td>IL</td>
            <td>2533.0</td>
        </tr>
        <tr>
            <td>Greene County Medical Center</td>
            <td>Jefferson</td>
            <td>IA</td>
            <td>2534.0</td>
        </tr>
        <tr>
            <td>Decatur County Hospital</td>
            <td>Leon</td>
            <td>IA</td>
            <td>2535.0</td>
        </tr>
        <tr>
            <td>Ottumwa Regional Health Center</td>
            <td>Ottumwa</td>
            <td>IA</td>
            <td>2536.0</td>
        </tr>
        <tr>
            <td>Tennova Healthcare-Newport Medical Center</td>
            <td>Newport</td>
            <td>TN</td>
            <td>2537.0</td>
        </tr>
        <tr>
            <td>Aurelia Osborn Fox Memorial Hospital</td>
            <td>Oneonta</td>
            <td>NY</td>
            <td>2538.0</td>
        </tr>
        <tr>
            <td>Carroll County Memorial Hospital</td>
            <td>Carrollton</td>
            <td>KY</td>
            <td>2539.0</td>
        </tr>
        <tr>
            <td>Calhoun-Liberty Hospital</td>
            <td>Blountstown</td>
            <td>FL</td>
            <td>2540.0</td>
        </tr>
        <tr>
            <td>CGH Medical Center</td>
            <td>Sterling</td>
            <td>IL</td>
            <td>2542.0</td>
        </tr>
        <tr>
            <td>H B Magruder Memorial Hospital</td>
            <td>Port Clinton</td>
            <td>OH</td>
            <td>2543.0</td>
        </tr>
        <tr>
            <td>Berger Hospital</td>
            <td>Circleville</td>
            <td>OH</td>
            <td>2544.0</td>
        </tr>
        <tr>
            <td>Rome Memorial Hospital</td>
            <td>Rome</td>
            <td>NY</td>
            <td>2546.0</td>
        </tr>
        <tr>
            <td>Rush Memorial Hospital</td>
            <td>Rushville</td>
            <td>IN</td>
            <td>2547.0</td>
        </tr>
        <tr>
            <td>Tift Regional Medical Center</td>
            <td>Tifton</td>
            <td>GA</td>
            <td>2548.0</td>
        </tr>
        <tr>
            <td>Whitesburg ARH Hospital</td>
            <td>Whitesburg</td>
            <td>KY</td>
            <td>2549.0</td>
        </tr>
        <tr>
            <td>USC Verdugo Hills Hospital</td>
            <td>Glendale</td>
            <td>CA</td>
            <td>2550.0</td>
        </tr>
        <tr>
            <td>Clay County Hospital</td>
            <td>Ashland</td>
            <td>AL</td>
            <td>2551.0</td>
        </tr>
        <tr>
            <td>Twin County Regional Hospital</td>
            <td>Galax</td>
            <td>VA</td>
            <td>2552.0</td>
        </tr>
        <tr>
            <td>Russellville Hospital</td>
            <td>Russellville</td>
            <td>AL</td>
            <td>2553.0</td>
        </tr>
        <tr>
            <td>Lexington Regional Health Center</td>
            <td>Lexington</td>
            <td>NE</td>
            <td>2554.0</td>
        </tr>
        <tr>
            <td>Bolivar Medical Center</td>
            <td>Cleveland</td>
            <td>MS</td>
            <td>2555.0</td>
        </tr>
        <tr>
            <td>Medical Center Barbour</td>
            <td>Eufaula</td>
            <td>AL</td>
            <td>2556.0</td>
        </tr>
        <tr>
            <td>Fort Duncan Medical Center</td>
            <td>Eagle Pass</td>
            <td>TX</td>
            <td>2557.0</td>
        </tr>
        <tr>
            <td>Braxton County Memorial Hospital</td>
            <td>Gassaway</td>
            <td>WV</td>
            <td>2558.0</td>
        </tr>
        <tr>
            <td>Colquitt Regional Medical Center</td>
            <td>Moultrie</td>
            <td>GA</td>
            <td>2559.0</td>
        </tr>
        <tr>
            <td>Summerlin Hospital Medical Center</td>
            <td>Las Vegas</td>
            <td>NV</td>
            <td>2560.0</td>
        </tr>
        <tr>
            <td>Winter Haven Hospital</td>
            <td>Winter Haven</td>
            <td>FL</td>
            <td>2561.0</td>
        </tr>
        <tr>
            <td>Raleigh General Hospital</td>
            <td>Beckley</td>
            <td>WV</td>
            <td>2562.0</td>
        </tr>
        <tr>
            <td>Natchitoches Regional Medical Center</td>
            <td>Natchitoches</td>
            <td>LA</td>
            <td>2563.0</td>
        </tr>
        <tr>
            <td>Cibola General Hospital</td>
            <td>Grants</td>
            <td>NM</td>
            <td>2564.0</td>
        </tr>
        <tr>
            <td>UNC Rockingham</td>
            <td>Eden</td>
            <td>NC</td>
            <td>2565.0</td>
        </tr>
        <tr>
            <td>Coosa Valley Medical Center</td>
            <td>Sylacauga</td>
            <td>AL</td>
            <td>2566.0</td>
        </tr>
        <tr>
            <td>Emanuel Medical Center</td>
            <td>Swainsboro</td>
            <td>GA</td>
            <td>2567.0</td>
        </tr>
        <tr>
            <td>Parkview Regional Hospital</td>
            <td>Mexia</td>
            <td>TX</td>
            <td>2568.0</td>
        </tr>
        <tr>
            <td>Iroquois Memorial Hospital</td>
            <td>Watseka</td>
            <td>IL</td>
            <td>2569.0</td>
        </tr>
        <tr>
            <td>AllianceHealth Ponca City</td>
            <td>Ponca City</td>
            <td>OK</td>
            <td>2570.0</td>
        </tr>
        <tr>
            <td>Glencoe Regional Health Services</td>
            <td>Glencoe</td>
            <td>MN</td>
            <td>2571.0</td>
        </tr>
        <tr>
            <td>Roseland Community Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>2572.0</td>
        </tr>
        <tr>
            <td>Parkview Wabash Hospital</td>
            <td>Wabash</td>
            <td>IN</td>
            <td>2573.0</td>
        </tr>
        <tr>
            <td>Alice Hyde Medical Center</td>
            <td>Malone</td>
            <td>NY</td>
            <td>2574.0</td>
        </tr>
        <tr>
            <td>Mena Regional Health System</td>
            <td>Mena</td>
            <td>AR</td>
            <td>2575.0</td>
        </tr>
        <tr>
            <td>Harrisburg Medical Center</td>
            <td>Harrisburg</td>
            <td>IL</td>
            <td>2576.0</td>
        </tr>
        <tr>
            <td>South Sunflower County Hospital</td>
            <td>Indianola</td>
            <td>MS</td>
            <td>2577.0</td>
        </tr>
        <tr>
            <td>Texas Health Presbyterian Hospital Kaufman</td>
            <td>Kaufman</td>
            <td>TX</td>
            <td>2578.0</td>
        </tr>
        <tr>
            <td>The Medical Center at Bowling Green</td>
            <td>Bowling Green</td>
            <td>KY</td>
            <td>2579.0</td>
        </tr>
        <tr>
            <td>Franklin Medical Center</td>
            <td>Winnsboro</td>
            <td>LA</td>
            <td>2580.0</td>
        </tr>
        <tr>
            <td>Anderson Regional Medical Center</td>
            <td>Meridian</td>
            <td>MS</td>
            <td>2581.0</td>
        </tr>
        <tr>
            <td>Big South Fork Medical Center</td>
            <td>Oneida</td>
            <td>TN</td>
            <td>2582.0</td>
        </tr>
        <tr>
            <td>Knox Community Hospital</td>
            <td>Mount Vernon</td>
            <td>OH</td>
            <td>2583.0</td>
        </tr>
        <tr>
            <td>Anderson County Hospital</td>
            <td>Garnett</td>
            <td>KS</td>
            <td>2584.0</td>
        </tr>
        <tr>
            <td>Southeast Health Center of Stoddard County</td>
            <td>Dexter</td>
            <td>MO</td>
            <td>2585.0</td>
        </tr>
        <tr>
            <td>Mercy One Elkader Medical Center</td>
            <td>Elkader</td>
            <td>IA</td>
            <td>2586.0</td>
        </tr>
        <tr>
            <td>Avera Gregory Hospital</td>
            <td>Gregory</td>
            <td>SD</td>
            <td>2587.0</td>
        </tr>
        <tr>
            <td>Donalsonville Hospital</td>
            <td>Donalsonville</td>
            <td>GA</td>
            <td>2588.0</td>
        </tr>
        <tr>
            <td>Essentia Health Northern Pines Medical Center</td>
            <td>Aurora</td>
            <td>MN</td>
            <td>2589.0</td>
        </tr>
        <tr>
            <td>Oak Valley Hospital District</td>
            <td>Oakdale</td>
            <td>CA</td>
            <td>2590.0</td>
        </tr>
        <tr>
            <td>Martin General Hospital</td>
            <td>Williamston</td>
            <td>NC</td>
            <td>2591.0</td>
        </tr>
        <tr>
            <td>Hazard ARH Regional Medical Center</td>
            <td>Hazard</td>
            <td>KY</td>
            <td>2592.0</td>
        </tr>
        <tr>
            <td>George Regional Health System</td>
            <td>Lucedale</td>
            <td>MS</td>
            <td>2593.0</td>
        </tr>
        <tr>
            <td>Val Verde Regional Medical Center</td>
            <td>Del Rio</td>
            <td>TX</td>
            <td>2594.0</td>
        </tr>
        <tr>
            <td>Milbank Area Hospital/Avera Health</td>
            <td>Milbank</td>
            <td>SD</td>
            <td>2595.0</td>
        </tr>
        <tr>
            <td>Savoy Medical Center</td>
            <td>Mamou</td>
            <td>LA</td>
            <td>2596.0</td>
        </tr>
        <tr>
            <td>Mitchell County Hospital District</td>
            <td>Colorado City</td>
            <td>TX</td>
            <td>2597.0</td>
        </tr>
        <tr>
            <td>Tug Valley ARH Regional Medical Center</td>
            <td>South Williamson</td>
            <td>KY</td>
            <td>2598.0</td>
        </tr>
        <tr>
            <td>Rice Medical Center</td>
            <td>Eagle Lake</td>
            <td>TX</td>
            <td>2599.0</td>
        </tr>
        <tr>
            <td>Washington County Hospital</td>
            <td>Chatom</td>
            <td>AL</td>
            <td>2600.0</td>
        </tr>
        <tr>
            <td>John C. Fremont Healthcare District</td>
            <td>Mariposa</td>
            <td>CA</td>
            <td>2601.0</td>
        </tr>
        <tr>
            <td>Stonewall Jackson Memorial Hospital</td>
            <td>Weston</td>
            <td>WV</td>
            <td>2602.0</td>
        </tr>
        <tr>
            <td>Clarke County Hospital</td>
            <td>Osceola</td>
            <td>IA</td>
            <td>2603.0</td>
        </tr>
        <tr>
            <td>Forrest City Medical Center</td>
            <td>Forrest City</td>
            <td>AR</td>
            <td>2604.0</td>
        </tr>
        <tr>
            <td>Arbor Health Morton Hospital</td>
            <td>Morton</td>
            <td>WA</td>
            <td>2605.0</td>
        </tr>
        <tr>
            <td>Helena Regional Medical Center</td>
            <td>Helena</td>
            <td>AR</td>
            <td>2606.0</td>
        </tr>
        <tr>
            <td>Hansen Family Hospital</td>
            <td>Iowa Falls</td>
            <td>IA</td>
            <td>2607.0</td>
        </tr>
        <tr>
            <td>Otto Kaiser Memorial Hospital</td>
            <td>Kenedy</td>
            <td>TX</td>
            <td>2608.0</td>
        </tr>
        <tr>
            <td>Sanford Tracy</td>
            <td>Tracy</td>
            <td>MN</td>
            <td>2609.0</td>
        </tr>
        <tr>
            <td>Metro Nashville General Hospital</td>
            <td>Nashville</td>
            <td>TN</td>
            <td>2610.0</td>
        </tr>
        <tr>
            <td>Skagit Valley Hospital</td>
            <td>Mount Vernon</td>
            <td>WA</td>
            <td>2611.0</td>
        </tr>
        <tr>
            <td>Central Washington Hospital</td>
            <td>Wenatchee</td>
            <td>WA</td>
            <td>2612.0</td>
        </tr>
        <tr>
            <td>Carepoint Health-Hoboken University Medical Center</td>
            <td>Hoboken</td>
            <td>NJ</td>
            <td>2613.0</td>
        </tr>
        <tr>
            <td>Mount Carmel West</td>
            <td>Columbus</td>
            <td>OH</td>
            <td>2614.0</td>
        </tr>
        <tr>
            <td>Abrazo Central Campus</td>
            <td>Phoenix</td>
            <td>AZ</td>
            <td>2615.0</td>
        </tr>
        <tr>
            <td>Raulerson Hospital</td>
            <td>Okeechobee</td>
            <td>FL</td>
            <td>2616.0</td>
        </tr>
        <tr>
            <td>Harris Regional Hospital</td>
            <td>Sylva</td>
            <td>NC</td>
            <td>2617.0</td>
        </tr>
        <tr>
            <td>Texas Health Harris Methodist Hospital Azle</td>
            <td>Azle</td>
            <td>TX</td>
            <td>2618.0</td>
        </tr>
        <tr>
            <td>Louis A. Weiss Memorial Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>2620.0</td>
        </tr>
        <tr>
            <td>Catskill Regional Medical Center</td>
            <td>Harris</td>
            <td>NY</td>
            <td>2621.0</td>
        </tr>
        <tr>
            <td>Matagorda Regional Medical Center</td>
            <td>Bay City</td>
            <td>TX</td>
            <td>2622.0</td>
        </tr>
        <tr>
            <td>United Memorial Medical Center</td>
            <td>Batavia</td>
            <td>NY</td>
            <td>2623.0</td>
        </tr>
        <tr>
            <td>Bronson Battle Creek Hospital</td>
            <td>Battle Creek</td>
            <td>MI</td>
            <td>2624.0</td>
        </tr>
        <tr>
            <td>Carilion Roanoke Memorial Hospital</td>
            <td>Roanoke</td>
            <td>VA</td>
            <td>2625.0</td>
        </tr>
        <tr>
            <td>Baystate Medical Center</td>
            <td>Springfield</td>
            <td>MA</td>
            <td>2626.0</td>
        </tr>
        <tr>
            <td>Euclid Hospital</td>
            <td>Euclid</td>
            <td>OH</td>
            <td>2627.0</td>
        </tr>
        <tr>
            <td>Tallahassee Memorial Hospital</td>
            <td>Tallahassee</td>
            <td>FL</td>
            <td>2628.0</td>
        </tr>
        <tr>
            <td>Holzer Medical Center</td>
            <td>Gallipolis</td>
            <td>OH</td>
            <td>2629.0</td>
        </tr>
        <tr>
            <td>Presence Mercy Medical Center</td>
            <td>Aurora</td>
            <td>IL</td>
            <td>2630.0</td>
        </tr>
        <tr>
            <td>Roger Williams Medical Center</td>
            <td>Providence</td>
            <td>RI</td>
            <td>2631.0</td>
        </tr>
        <tr>
            <td>Kaleida Health</td>
            <td>Buffalo</td>
            <td>NY</td>
            <td>2632.0</td>
        </tr>
        <tr>
            <td>M Health Fairview University of Minnesota Medical Center</td>
            <td>Minneapolis</td>
            <td>MN</td>
            <td>2633.0</td>
        </tr>
        <tr>
            <td>Minden Medical Center</td>
            <td>Minden</td>
            <td>LA</td>
            <td>2634.0</td>
        </tr>
        <tr>
            <td>Northeastern Nevada Regional Hospital</td>
            <td>Elko</td>
            <td>NV</td>
            <td>2635.0</td>
        </tr>
        <tr>
            <td>Geneva General Hospital</td>
            <td>Geneva</td>
            <td>NY</td>
            <td>2636.0</td>
        </tr>
        <tr>
            <td>Marcum &amp; Wallace Memorial Hospital</td>
            <td>Irvine</td>
            <td>KY</td>
            <td>2638.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital Los Banos</td>
            <td>Los Banos</td>
            <td>CA</td>
            <td>2639.0</td>
        </tr>
        <tr>
            <td>St. Joseph Regional Medical Center</td>
            <td>Lewiston</td>
            <td>ID</td>
            <td>2640.0</td>
        </tr>
        <tr>
            <td>Trinity Hospitals</td>
            <td>Minot</td>
            <td>ND</td>
            <td>2641.0</td>
        </tr>
        <tr>
            <td>Comanche County Memorial Hospital</td>
            <td>Lawton</td>
            <td>OK</td>
            <td>2642.0</td>
        </tr>
        <tr>
            <td>St. Catherine of Siena Hospital</td>
            <td>Smithtown</td>
            <td>NY</td>
            <td>2643.0</td>
        </tr>
        <tr>
            <td>Our Lady of Fatima Hospital</td>
            <td>North Providence</td>
            <td>RI</td>
            <td>2644.0</td>
        </tr>
        <tr>
            <td>Cape Regional Medical Center</td>
            <td>Cape May Court House</td>
            <td>NJ</td>
            <td>2646.0</td>
        </tr>
        <tr>
            <td>Kendall Regional Medical Center</td>
            <td>Miami</td>
            <td>FL</td>
            <td>2647.0</td>
        </tr>
        <tr>
            <td>Southcoast Hospitals Group</td>
            <td>Fall River</td>
            <td>MA</td>
            <td>2648.0</td>
        </tr>
        <tr>
            <td>Conemaugh Memorial Medical Center</td>
            <td>Johnstown</td>
            <td>PA</td>
            <td>2649.0</td>
        </tr>
        <tr>
            <td>Coast Plaza Hospital</td>
            <td>Norwalk</td>
            <td>CA</td>
            <td>2650.0</td>
        </tr>
        <tr>
            <td>Baptist Memorial Hospital</td>
            <td>Memphis</td>
            <td>TN</td>
            <td>2651.0</td>
        </tr>
        <tr>
            <td>Jennings American Legion Hospital</td>
            <td>Jennings</td>
            <td>LA</td>
            <td>2652.0</td>
        </tr>
        <tr>
            <td>Decatur Memorial Hospital</td>
            <td>Decatur</td>
            <td>IL</td>
            <td>2653.0</td>
        </tr>
        <tr>
            <td>University Medical Center</td>
            <td>Las Vegas</td>
            <td>NV</td>
            <td>2654.0</td>
        </tr>
        <tr>
            <td>Oakbend Medical Center</td>
            <td>Richmond</td>
            <td>TX</td>
            <td>2655.0</td>
        </tr>
        <tr>
            <td>Guadalupe Regional Medical Center</td>
            <td>Seguin</td>
            <td>TX</td>
            <td>2656.0</td>
        </tr>
        <tr>
            <td>Bartow Regional Medical Center</td>
            <td>Bartow</td>
            <td>FL</td>
            <td>2657.0</td>
        </tr>
        <tr>
            <td>Southwest Medical Center</td>
            <td>Liberal</td>
            <td>KS</td>
            <td>2658.0</td>
        </tr>
        <tr>
            <td>Aurora Medical Center Manitowoc County</td>
            <td>Two Rivers</td>
            <td>WI</td>
            <td>2659.0</td>
        </tr>
        <tr>
            <td>Oklahoma State University Medical Center</td>
            <td>Tulsa</td>
            <td>OK</td>
            <td>2660.0</td>
        </tr>
        <tr>
            <td>Highland CommunityÂ¬â€  Hospital</td>
            <td>Picayune</td>
            <td>MS</td>
            <td>2661.0</td>
        </tr>
        <tr>
            <td>Fort Washington Hospital</td>
            <td>Fort Washington</td>
            <td>MD</td>
            <td>2662.0</td>
        </tr>
        <tr>
            <td>Glendale Memorial Hospital &amp; Health Center</td>
            <td>Glendale</td>
            <td>CA</td>
            <td>2663.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital at Gulfport</td>
            <td>Gulfport</td>
            <td>MS</td>
            <td>2664.0</td>
        </tr>
        <tr>
            <td>St. Vincent&#x27;s St. Clair</td>
            <td>Pell City</td>
            <td>AL</td>
            <td>2665.0</td>
        </tr>
        <tr>
            <td>South Florida Baptist Hospital</td>
            <td>Plant City</td>
            <td>FL</td>
            <td>2666.0</td>
        </tr>
        <tr>
            <td>Tanner Medical Center Villa Rica</td>
            <td>Villa Rica</td>
            <td>GA</td>
            <td>2667.0</td>
        </tr>
        <tr>
            <td>West Hills Hospital &amp; Medical Center</td>
            <td>West Hills</td>
            <td>CA</td>
            <td>2668.0</td>
        </tr>
        <tr>
            <td>Carlsbad Medical Center</td>
            <td>Carlsbad</td>
            <td>NM</td>
            <td>2669.0</td>
        </tr>
        <tr>
            <td>Ochsner LSU Health Shreveport</td>
            <td>Shreveport</td>
            <td>LA</td>
            <td>2670.0</td>
        </tr>
        <tr>
            <td>Piedmont Walton Hospital</td>
            <td>Monroe</td>
            <td>GA</td>
            <td>2671.0</td>
        </tr>
        <tr>
            <td>El Centro Regional Medical Center</td>
            <td>El Centro</td>
            <td>CA</td>
            <td>2672.0</td>
        </tr>
        <tr>
            <td>Mimbres Memorial Hospital</td>
            <td>Deming</td>
            <td>NM</td>
            <td>2673.0</td>
        </tr>
        <tr>
            <td>Sturdy Memorial Hospital</td>
            <td>Attleboro</td>
            <td>MA</td>
            <td>2674.0</td>
        </tr>
        <tr>
            <td>Boone County Health Center</td>
            <td>Albion</td>
            <td>NE</td>
            <td>2675.0</td>
        </tr>
        <tr>
            <td>Sierra View Medical Center</td>
            <td>Porterville</td>
            <td>CA</td>
            <td>2676.0</td>
        </tr>
        <tr>
            <td>Grant Regional Health Center</td>
            <td>Lancaster</td>
            <td>WI</td>
            <td>2677.0</td>
        </tr>
        <tr>
            <td>Faxton-St. Luke&#x27;s Healthcare</td>
            <td>Utica</td>
            <td>NY</td>
            <td>2678.0</td>
        </tr>
        <tr>
            <td>Myrtue Medical Center</td>
            <td>Harlan</td>
            <td>IA</td>
            <td>2679.0</td>
        </tr>
        <tr>
            <td>Staten Island University Hospital</td>
            <td>Staten Island</td>
            <td>NY</td>
            <td>2680.0</td>
        </tr>
        <tr>
            <td>OSF Heart of Mary Medical Center</td>
            <td>Urbana</td>
            <td>IL</td>
            <td>2681.0</td>
        </tr>
        <tr>
            <td>Lakeside Medical Center</td>
            <td>Belle Glade</td>
            <td>FL</td>
            <td>2682.0</td>
        </tr>
        <tr>
            <td>Central Peninsula General Hospital</td>
            <td>Soldotna</td>
            <td>AK</td>
            <td>2683.0</td>
        </tr>
        <tr>
            <td>Forrest General Hospital</td>
            <td>Hattiesburg</td>
            <td>MS</td>
            <td>2684.0</td>
        </tr>
        <tr>
            <td>Huntsville Memorial Hospital</td>
            <td>Huntsville</td>
            <td>TX</td>
            <td>2685.0</td>
        </tr>
        <tr>
            <td>Christus Spohn Hospital Beeville</td>
            <td>Beeville</td>
            <td>TX</td>
            <td>2686.0</td>
        </tr>
        <tr>
            <td>Uniontown Hospital</td>
            <td>Uniontown</td>
            <td>PA</td>
            <td>2687.0</td>
        </tr>
        <tr>
            <td>Montefiore New Rochelle Hospital</td>
            <td>New Rochelle</td>
            <td>NY</td>
            <td>2688.0</td>
        </tr>
        <tr>
            <td>Sioux Center Health</td>
            <td>Sioux Center</td>
            <td>IA</td>
            <td>2689.0</td>
        </tr>
        <tr>
            <td>Touchette Regional Hospital</td>
            <td>Centreville</td>
            <td>IL</td>
            <td>2690.0</td>
        </tr>
        <tr>
            <td>South Shore Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>2691.0</td>
        </tr>
        <tr>
            <td>Hackensack-UMC Mountainside</td>
            <td>Montclair</td>
            <td>NJ</td>
            <td>2692.0</td>
        </tr>
        <tr>
            <td>Regional One Health</td>
            <td>Memphis</td>
            <td>TN</td>
            <td>2693.0</td>
        </tr>
        <tr>
            <td>Republic County Hospital</td>
            <td>Belleville</td>
            <td>KS</td>
            <td>2694.0</td>
        </tr>
        <tr>
            <td>University Medical Center of El Paso</td>
            <td>El Paso</td>
            <td>TX</td>
            <td>2695.0</td>
        </tr>
        <tr>
            <td>Mcdowell ARH Hospital</td>
            <td>McDowell</td>
            <td>KY</td>
            <td>2696.0</td>
        </tr>
        <tr>
            <td>Palmetto General Hospital</td>
            <td>Hialeah</td>
            <td>FL</td>
            <td>2697.0</td>
        </tr>
        <tr>
            <td>Chenango Memorial Hospital</td>
            <td>Norwich</td>
            <td>NY</td>
            <td>2698.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Cassville</td>
            <td>Cassville</td>
            <td>MO</td>
            <td>2699.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Berryville</td>
            <td>Berryville</td>
            <td>AR</td>
            <td>2700.0</td>
        </tr>
        <tr>
            <td>Starr County Memorial Hospital</td>
            <td>Rio Grande City</td>
            <td>TX</td>
            <td>2702.0</td>
        </tr>
        <tr>
            <td>Hayward Area Memorial Hospital</td>
            <td>Hayward</td>
            <td>WI</td>
            <td>2703.0</td>
        </tr>
        <tr>
            <td>Beauregard Memorial Hospital</td>
            <td>Deridder</td>
            <td>LA</td>
            <td>2705.0</td>
        </tr>
        <tr>
            <td>Wyoming County Community Hospital</td>
            <td>Warsaw</td>
            <td>NY</td>
            <td>2706.0</td>
        </tr>
        <tr>
            <td>Jay Hospital</td>
            <td>Jay</td>
            <td>FL</td>
            <td>2707.0</td>
        </tr>
        <tr>
            <td>Brownfield Regional Medical Center</td>
            <td>Brownfield</td>
            <td>TX</td>
            <td>2708.0</td>
        </tr>
        <tr>
            <td>Adventist Health Reedley</td>
            <td>Reedley</td>
            <td>CA</td>
            <td>2709.0</td>
        </tr>
        <tr>
            <td>T. J. Health Columbia</td>
            <td>Columbia</td>
            <td>KY</td>
            <td>2710.0</td>
        </tr>
        <tr>
            <td>Freestone Medical Center</td>
            <td>Fairfield</td>
            <td>TX</td>
            <td>2711.0</td>
        </tr>
        <tr>
            <td>McLeod Medical Center - Dillon</td>
            <td>Dillon</td>
            <td>SC</td>
            <td>2712.0</td>
        </tr>
        <tr>
            <td>Palo Pinto General Hospital</td>
            <td>Mineral Wells</td>
            <td>TX</td>
            <td>2713.0</td>
        </tr>
        <tr>
            <td>Christus Mother Frances Hospital- Jacksonville</td>
            <td>Jacksonville</td>
            <td>TX</td>
            <td>2716.0</td>
        </tr>
        <tr>
            <td>Harrison Memorial Hospital</td>
            <td>Cynthiana</td>
            <td>KY</td>
            <td>2717.0</td>
        </tr>
        <tr>
            <td>Adena Pike Medical Center</td>
            <td>Waverly</td>
            <td>OH</td>
            <td>2718.0</td>
        </tr>
        <tr>
            <td>Upper Connecticut Valley Hospital</td>
            <td>Colebrook</td>
            <td>NH</td>
            <td>2719.0</td>
        </tr>
        <tr>
            <td>Shenandoah Medical Center</td>
            <td>Shenandoah</td>
            <td>IA</td>
            <td>2720.0</td>
        </tr>
        <tr>
            <td>Walthall County General Hospital</td>
            <td>Tylertown</td>
            <td>MS</td>
            <td>2721.0</td>
        </tr>
        <tr>
            <td>Wilbarger General Hospital</td>
            <td>Vernon</td>
            <td>TX</td>
            <td>2722.0</td>
        </tr>
        <tr>
            <td>The Medical Center at Franklin</td>
            <td>Franklin</td>
            <td>KY</td>
            <td>2723.0</td>
        </tr>
        <tr>
            <td>Clay County Memorial Hospital</td>
            <td>Henrietta</td>
            <td>TX</td>
            <td>2724.0</td>
        </tr>
        <tr>
            <td>Nevada Regional Medical Center</td>
            <td>Nevada</td>
            <td>MO</td>
            <td>2725.0</td>
        </tr>
        <tr>
            <td>Medina Regional Hospital</td>
            <td>Hondo</td>
            <td>TX</td>
            <td>2727.0</td>
        </tr>
        <tr>
            <td>Welch Community Hospital</td>
            <td>Welch</td>
            <td>WV</td>
            <td>2728.0</td>
        </tr>
        <tr>
            <td>Erlanger Bledsoe Hospital</td>
            <td>Pikeville</td>
            <td>TN</td>
            <td>2729.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System - St. James</td>
            <td>St. James</td>
            <td>MN</td>
            <td>2730.0</td>
        </tr>
        <tr>
            <td>Hi-Desert Medical Center</td>
            <td>Joshua Tree</td>
            <td>CA</td>
            <td>2731.0</td>
        </tr>
        <tr>
            <td>Pawnee Valley Community Hospital</td>
            <td>Larned</td>
            <td>KS</td>
            <td>2732.0</td>
        </tr>
        <tr>
            <td>Medical Arts Hospital</td>
            <td>Lamesa</td>
            <td>TX</td>
            <td>2733.0</td>
        </tr>
        <tr>
            <td>Swain County Hospital</td>
            <td>Bryson City</td>
            <td>NC</td>
            <td>2734.0</td>
        </tr>
        <tr>
            <td>Mary Breckinridge ARH Hospital</td>
            <td>Hyden</td>
            <td>KY</td>
            <td>2735.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Ozark</td>
            <td>Ozark</td>
            <td>AR</td>
            <td>2737.0</td>
        </tr>
        <tr>
            <td>Faith Community Hospital</td>
            <td>Jacksboro</td>
            <td>TX</td>
            <td>2738.0</td>
        </tr>
        <tr>
            <td>Desoto Regional Health System</td>
            <td>Mansfield</td>
            <td>LA</td>
            <td>2739.0</td>
        </tr>
        <tr>
            <td>Hardin Medical Center</td>
            <td>Savannah</td>
            <td>TN</td>
            <td>2741.0</td>
        </tr>
        <tr>
            <td>Avera Gettysburg Hospital</td>
            <td>Gettysburg</td>
            <td>SD</td>
            <td>2742.0</td>
        </tr>
        <tr>
            <td>Glendive Medical Center</td>
            <td>Glendive</td>
            <td>MT</td>
            <td>2743.0</td>
        </tr>
        <tr>
            <td>San Luis Valley Health Conejos County Hospital</td>
            <td>La Jara</td>
            <td>CO</td>
            <td>2744.0</td>
        </tr>
        <tr>
            <td>Moundview Memorial Hospital and Clinics</td>
            <td>Friendship</td>
            <td>WI</td>
            <td>2745.0</td>
        </tr>
        <tr>
            <td>Optim Medical Center - Screven</td>
            <td>Sylvania</td>
            <td>GA</td>
            <td>2746.0</td>
        </tr>
        <tr>
            <td>Baptist Medical Center-Leake</td>
            <td>Carthage</td>
            <td>MS</td>
            <td>2747.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital of Franciscan Sisters-Oelwein</td>
            <td>Oelwein</td>
            <td>IA</td>
            <td>2748.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Clermont</td>
            <td>Batavia</td>
            <td>OH</td>
            <td>2749.0</td>
        </tr>
        <tr>
            <td>Poinciana Medical Center</td>
            <td>Kissimmee</td>
            <td>FL</td>
            <td>2750.0</td>
        </tr>
        <tr>
            <td>St. Mary Medical Center</td>
            <td>Galesburg</td>
            <td>IL</td>
            <td>2751.0</td>
        </tr>
        <tr>
            <td>Texoma Medical Center</td>
            <td>Denison</td>
            <td>TX</td>
            <td>2753.0</td>
        </tr>
        <tr>
            <td>Valley Presbyterian Hospital</td>
            <td>Van Nuys</td>
            <td>CA</td>
            <td>2754.0</td>
        </tr>
        <tr>
            <td>Prairie Lakes Healthcare System</td>
            <td>Watertown</td>
            <td>SD</td>
            <td>2755.0</td>
        </tr>
        <tr>
            <td>SSM Health Saint Louis University Hospital</td>
            <td>Saint Louis</td>
            <td>MO</td>
            <td>2756.0</td>
        </tr>
        <tr>
            <td>Saint Mary&#x27;s Hospital</td>
            <td>Waterbury</td>
            <td>CT</td>
            <td>2757.0</td>
        </tr>
        <tr>
            <td>Lake City Medical Center</td>
            <td>Lake City</td>
            <td>FL</td>
            <td>2758.0</td>
        </tr>
        <tr>
            <td>St. Mary&#x27;s of Michigan Medical Center</td>
            <td>Saginaw</td>
            <td>MI</td>
            <td>2759.0</td>
        </tr>
        <tr>
            <td>Geisinger Wyoming Valley Medical Center</td>
            <td>Wilkes Barre</td>
            <td>PA</td>
            <td>2760.0</td>
        </tr>
        <tr>
            <td>SSM Health Depaul Hospital St. Louis</td>
            <td>Bridgeton</td>
            <td>MO</td>
            <td>2761.0</td>
        </tr>
        <tr>
            <td>Washington Hospital</td>
            <td>Fremont</td>
            <td>CA</td>
            <td>2762.0</td>
        </tr>
        <tr>
            <td>Integris Canadian Valley Hospital</td>
            <td>Yukon</td>
            <td>OK</td>
            <td>2763.0</td>
        </tr>
        <tr>
            <td>Granville Health Systems</td>
            <td>Oxford</td>
            <td>NC</td>
            <td>2764.0</td>
        </tr>
        <tr>
            <td>Southern Virginia Regional Medical Center</td>
            <td>Emporia</td>
            <td>VA</td>
            <td>2765.0</td>
        </tr>
        <tr>
            <td>St. Joseph Medical Center</td>
            <td>Bloomington</td>
            <td>IL</td>
            <td>2766.0</td>
        </tr>
        <tr>
            <td>The Medical Center, Navicent Health</td>
            <td>Macon</td>
            <td>GA</td>
            <td>2767.0</td>
        </tr>
        <tr>
            <td>Bristol Regional Medical Center</td>
            <td>Bristol</td>
            <td>TN</td>
            <td>2768.0</td>
        </tr>
        <tr>
            <td>Piedmont Columbus Regional Midtown</td>
            <td>Columbus</td>
            <td>GA</td>
            <td>2769.0</td>
        </tr>
        <tr>
            <td>Covenant Medical Center</td>
            <td>Waterloo</td>
            <td>IA</td>
            <td>2770.0</td>
        </tr>
        <tr>
            <td>Manatee Memorial Hospital</td>
            <td>Bradenton</td>
            <td>FL</td>
            <td>2771.0</td>
        </tr>
        <tr>
            <td>Nyack Hospital</td>
            <td>Nyack</td>
            <td>NY</td>
            <td>2772.0</td>
        </tr>
        <tr>
            <td>Nazareth Hospital</td>
            <td>Philadelphia</td>
            <td>PA</td>
            <td>2773.0</td>
        </tr>
        <tr>
            <td>Lake Charles Memorial Hospital</td>
            <td>Lake Charles</td>
            <td>LA</td>
            <td>2774.0</td>
        </tr>
        <tr>
            <td>Iberia Medical Center</td>
            <td>New Iberia</td>
            <td>LA</td>
            <td>2775.0</td>
        </tr>
        <tr>
            <td>Southeast Georgia Health System- Brunswick Campus</td>
            <td>Brunswick</td>
            <td>GA</td>
            <td>2776.0</td>
        </tr>
        <tr>
            <td>North Arkansas Regional Medical Center</td>
            <td>Harrison</td>
            <td>AR</td>
            <td>2777.0</td>
        </tr>
        <tr>
            <td>Holyoke Medical Center</td>
            <td>Holyoke</td>
            <td>MA</td>
            <td>2778.0</td>
        </tr>
        <tr>
            <td>Bayfront Health Brooksville</td>
            <td>Brooksville</td>
            <td>FL</td>
            <td>2779.0</td>
        </tr>
        <tr>
            <td>Pekin Memorial Hospital</td>
            <td>Pekin</td>
            <td>IL</td>
            <td>2780.0</td>
        </tr>
        <tr>
            <td>Fillmore County Hospital</td>
            <td>Geneva</td>
            <td>NE</td>
            <td>2781.0</td>
        </tr>
        <tr>
            <td>Medstar Harbor Hospital</td>
            <td>Baltimore</td>
            <td>MD</td>
            <td>2782.0</td>
        </tr>
        <tr>
            <td>Union County Hospital</td>
            <td>Anna</td>
            <td>IL</td>
            <td>2783.0</td>
        </tr>
        <tr>
            <td>Roosevelt General Hospital</td>
            <td>Portales</td>
            <td>NM</td>
            <td>2784.0</td>
        </tr>
        <tr>
            <td>El Campo Memorial Hospital</td>
            <td>El Campo</td>
            <td>TX</td>
            <td>2785.0</td>
        </tr>
        <tr>
            <td>Rio Grande Hospital</td>
            <td>Del Norte</td>
            <td>CO</td>
            <td>2786.0</td>
        </tr>
        <tr>
            <td>Aiken Regional Medical Center</td>
            <td>Aiken</td>
            <td>SC</td>
            <td>2787.0</td>
        </tr>
        <tr>
            <td>Community Hospital of Huntington Park</td>
            <td>Huntington Park</td>
            <td>CA</td>
            <td>2788.0</td>
        </tr>
        <tr>
            <td>Mercy Medical Center-Sioux City</td>
            <td>Sioux City</td>
            <td>IA</td>
            <td>2789.0</td>
        </tr>
        <tr>
            <td>Midmichigan Medical Center-Gratiot</td>
            <td>Alma</td>
            <td>MI</td>
            <td>2790.0</td>
        </tr>
        <tr>
            <td>Winona Health Services</td>
            <td>Winona</td>
            <td>MN</td>
            <td>2791.0</td>
        </tr>
        <tr>
            <td>Marshall Medical Center South</td>
            <td>Boaz</td>
            <td>AL</td>
            <td>2792.0</td>
        </tr>
        <tr>
            <td>Avera St. Benedict Health Center - Cah</td>
            <td>Parkston</td>
            <td>SD</td>
            <td>2793.0</td>
        </tr>
        <tr>
            <td>Hegg Memorial Health Center</td>
            <td>Rock Valley</td>
            <td>IA</td>
            <td>2794.0</td>
        </tr>
        <tr>
            <td>Southwest Mississippi Regional Medical Center</td>
            <td>McConnellsburg</td>
            <td>MS</td>
            <td>2795.0</td>
        </tr>
        <tr>
            <td>Niagara Falls Memorial Medical Center</td>
            <td>Niagara Falls</td>
            <td>NY</td>
            <td>2796.0</td>
        </tr>
        <tr>
            <td>Brooks Memorial Hospital</td>
            <td>Dunkirk</td>
            <td>NY</td>
            <td>2797.0</td>
        </tr>
        <tr>
            <td>Abrom Kaplan Memorial Hospital</td>
            <td>Kaplan</td>
            <td>LA</td>
            <td>2798.0</td>
        </tr>
        <tr>
            <td>Kearny County Hospital</td>
            <td>Lakin</td>
            <td>KS</td>
            <td>2800.0</td>
        </tr>
        <tr>
            <td>Bath Community Hospital</td>
            <td>Hot Springs</td>
            <td>VA</td>
            <td>2801.0</td>
        </tr>
        <tr>
            <td>Allen Parish Hospital</td>
            <td>Kinder</td>
            <td>LA</td>
            <td>2802.0</td>
        </tr>
        <tr>
            <td>Stephens County Hospital</td>
            <td>Toccoa</td>
            <td>GA</td>
            <td>2803.0</td>
        </tr>
        <tr>
            <td>Hannibal Regional Hospital</td>
            <td>Hannibal</td>
            <td>MO</td>
            <td>2804.0</td>
        </tr>
        <tr>
            <td>Arkansas Valley Regional Medical Center</td>
            <td>La Junta</td>
            <td>CO</td>
            <td>2805.0</td>
        </tr>
        <tr>
            <td>Chatuge Regional Hospital</td>
            <td>Hiawassee</td>
            <td>GA</td>
            <td>2806.0</td>
        </tr>
        <tr>
            <td>West River Regional Medical Center</td>
            <td>Hettinger</td>
            <td>ND</td>
            <td>2807.0</td>
        </tr>
        <tr>
            <td>New London Hospital</td>
            <td>New London</td>
            <td>NH</td>
            <td>2808.0</td>
        </tr>
        <tr>
            <td>Rehoboth Mckinley Christian Health Care Services</td>
            <td>Gallup</td>
            <td>NM</td>
            <td>2809.0</td>
        </tr>
        <tr>
            <td>Penobscot Valley Hospital</td>
            <td>Lincoln</td>
            <td>ME</td>
            <td>2810.0</td>
        </tr>
        <tr>
            <td>Cumberland Memorial Hospital</td>
            <td>Cumberland</td>
            <td>WI</td>
            <td>2811.0</td>
        </tr>
        <tr>
            <td>Heart Of America Medical Center</td>
            <td>Rugby</td>
            <td>ND</td>
            <td>2812.0</td>
        </tr>
        <tr>
            <td>Springfield Hospital</td>
            <td>Springfield</td>
            <td>VT</td>
            <td>2813.0</td>
        </tr>
        <tr>
            <td>Ozarks Community Hospital of Gravette</td>
            <td>Gravette</td>
            <td>AR</td>
            <td>2814.0</td>
        </tr>
        <tr>
            <td>Methodist Hospital of Chicago</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>2815.0</td>
        </tr>
        <tr>
            <td>St. Anthony Regional Hospital &amp; Nursing Home</td>
            <td>Carroll</td>
            <td>IA</td>
            <td>2816.0</td>
        </tr>
        <tr>
            <td>Little Colorado Medical Center</td>
            <td>Winslow</td>
            <td>AZ</td>
            <td>2817.0</td>
        </tr>
        <tr>
            <td>Grove Hill Memorial Hospital</td>
            <td>Grove Hill</td>
            <td>AL</td>
            <td>2818.0</td>
        </tr>
        <tr>
            <td>Lackey Memorial Hospital</td>
            <td>Forest</td>
            <td>MS</td>
            <td>2819.0</td>
        </tr>
        <tr>
            <td>Muscogee (Creek) Nation Medical Center</td>
            <td>Okmulgee</td>
            <td>OK</td>
            <td>2820.0</td>
        </tr>
        <tr>
            <td>Venice Regional Medical Center - Bayfront Health</td>
            <td>Venice</td>
            <td>FL</td>
            <td>2821.0</td>
        </tr>
        <tr>
            <td>Hamilton Hospital</td>
            <td>Olney</td>
            <td>TX</td>
            <td>2822.0</td>
        </tr>
        <tr>
            <td>St. Alexius Hospital</td>
            <td>Saint Louis</td>
            <td>MO</td>
            <td>2823.0</td>
        </tr>
        <tr>
            <td>Pacifica Hospital of the Valley</td>
            <td>Sun Valley</td>
            <td>CA</td>
            <td>2824.0</td>
        </tr>
        <tr>
            <td>Eaton Rapids Medical Center</td>
            <td>Eaton Rapids</td>
            <td>MI</td>
            <td>2825.0</td>
        </tr>
        <tr>
            <td>Ripon Medical Center</td>
            <td>Ripon</td>
            <td>WI</td>
            <td>2826.0</td>
        </tr>
        <tr>
            <td>Athens Limestone Hospital</td>
            <td>Athens</td>
            <td>AL</td>
            <td>2827.0</td>
        </tr>
        <tr>
            <td>Mountain West Medical Center</td>
            <td>Tooele</td>
            <td>UT</td>
            <td>2828.0</td>
        </tr>
        <tr>
            <td>Punxsutawney Area Hospital</td>
            <td>Punxsutawney</td>
            <td>PA</td>
            <td>2829.0</td>
        </tr>
        <tr>
            <td>Morton Plant Hospital</td>
            <td>Clearwater</td>
            <td>FL</td>
            <td>2830.0</td>
        </tr>
        <tr>
            <td>Childress Regional Medical Center</td>
            <td>Childress</td>
            <td>TX</td>
            <td>2831.0</td>
        </tr>
        <tr>
            <td>Thibodaux Regional Medical Center</td>
            <td>Thibodaux</td>
            <td>LA</td>
            <td>2832.0</td>
        </tr>
        <tr>
            <td>Lafayette General Medical Center</td>
            <td>Lafayette</td>
            <td>LA</td>
            <td>2833.0</td>
        </tr>
        <tr>
            <td>Ohiohealth Shelby Hospital</td>
            <td>Shelby</td>
            <td>OH</td>
            <td>2835.0</td>
        </tr>
        <tr>
            <td>Lewis County General Hospital</td>
            <td>Lowville</td>
            <td>NY</td>
            <td>2836.0</td>
        </tr>
        <tr>
            <td>Moses Taylor Hospital</td>
            <td>Scranton</td>
            <td>PA</td>
            <td>2837.0</td>
        </tr>
        <tr>
            <td>Los Alamos Medical Center</td>
            <td>Los Alamos</td>
            <td>NM</td>
            <td>2838.0</td>
        </tr>
        <tr>
            <td>Baptist Health Paducah</td>
            <td>Paducah</td>
            <td>KY</td>
            <td>2839.0</td>
        </tr>
        <tr>
            <td>CHI St. Vincent Hospital Hot Springs</td>
            <td>Hot Springs</td>
            <td>AR</td>
            <td>2840.0</td>
        </tr>
        <tr>
            <td>Copley Memorial Hospital</td>
            <td>Aurora</td>
            <td>IL</td>
            <td>2841.0</td>
        </tr>
        <tr>
            <td>Lonesome Pine Hospital</td>
            <td>Big Stone Gap</td>
            <td>VA</td>
            <td>2842.0</td>
        </tr>
        <tr>
            <td>Helen Keller Memorial Hospital</td>
            <td>Sheffield</td>
            <td>AL</td>
            <td>2843.0</td>
        </tr>
        <tr>
            <td>Rappahannock General Hospital</td>
            <td>Kilmarnock</td>
            <td>VA</td>
            <td>2844.0</td>
        </tr>
        <tr>
            <td>Dickinson County Memorial Hospital</td>
            <td>Iron Mountain</td>
            <td>MI</td>
            <td>2845.0</td>
        </tr>
        <tr>
            <td>Soin Medical Center</td>
            <td>Beaver Creek</td>
            <td>OH</td>
            <td>2846.0</td>
        </tr>
        <tr>
            <td>Cannon Memorial Hospital</td>
            <td>Pickens</td>
            <td>SC</td>
            <td>2847.0</td>
        </tr>
        <tr>
            <td>North Mississippi Medical Center</td>
            <td>Tupelo</td>
            <td>MS</td>
            <td>2848.0</td>
        </tr>
        <tr>
            <td>Westside Regional Medical Center</td>
            <td>Plantation</td>
            <td>FL</td>
            <td>2849.0</td>
        </tr>
        <tr>
            <td>Norton Hospital</td>
            <td>Louisville</td>
            <td>KY</td>
            <td>2850.0</td>
        </tr>
        <tr>
            <td>Jackson County Memorial Hospital Authority</td>
            <td>Altus</td>
            <td>OK</td>
            <td>2851.0</td>
        </tr>
        <tr>
            <td>Mercy Health-Allen Hospital</td>
            <td>Oberlin</td>
            <td>OH</td>
            <td>2852.0</td>
        </tr>
        <tr>
            <td>Rutherford Regional Medical Center</td>
            <td>Rutherfordton</td>
            <td>NC</td>
            <td>2853.0</td>
        </tr>
        <tr>
            <td>Lock Haven Hospital</td>
            <td>Lock Haven</td>
            <td>PA</td>
            <td>2855.0</td>
        </tr>
        <tr>
            <td>Christus Santa Rosa Medical Center</td>
            <td>San Antonio</td>
            <td>TX</td>
            <td>2856.0</td>
        </tr>
        <tr>
            <td>Ouachita County Medical Center</td>
            <td>Camden</td>
            <td>AR</td>
            <td>2857.0</td>
        </tr>
        <tr>
            <td>Duncan Regional Hospital</td>
            <td>Duncan</td>
            <td>OK</td>
            <td>2859.0</td>
        </tr>
        <tr>
            <td>Mercy Health - St. Joseph Warren Hospital</td>
            <td>Warren</td>
            <td>OH</td>
            <td>2860.0</td>
        </tr>
        <tr>
            <td>AdventHealth Palm Coast</td>
            <td>Palm Coast</td>
            <td>FL</td>
            <td>2861.0</td>
        </tr>
        <tr>
            <td>Titus Regional Medical Center</td>
            <td>Mount Pleasant</td>
            <td>TX</td>
            <td>2862.0</td>
        </tr>
        <tr>
            <td>St. Bernard Parish Hospital</td>
            <td>Chalmette</td>
            <td>LA</td>
            <td>2863.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital</td>
            <td>Belleville</td>
            <td>IL</td>
            <td>2864.0</td>
        </tr>
        <tr>
            <td>Newton Medical Center</td>
            <td>Newton</td>
            <td>KS</td>
            <td>2865.0</td>
        </tr>
        <tr>
            <td>St. Anthonys Hospital</td>
            <td>Saint Petersburg</td>
            <td>FL</td>
            <td>2866.0</td>
        </tr>
        <tr>
            <td>Good Samaritan Hospital Medical Center</td>
            <td>West Islip</td>
            <td>NY</td>
            <td>2867.0</td>
        </tr>
        <tr>
            <td>Carolinas Hospital System</td>
            <td>Florence</td>
            <td>SC</td>
            <td>2868.0</td>
        </tr>
        <tr>
            <td>Carteret General Hospital</td>
            <td>Morehead City</td>
            <td>NC</td>
            <td>2869.0</td>
        </tr>
        <tr>
            <td>St. Francis Medical Center</td>
            <td>Monroe</td>
            <td>LA</td>
            <td>2870.0</td>
        </tr>
        <tr>
            <td>Speare Memorial Hospital</td>
            <td>Plymouth</td>
            <td>NH</td>
            <td>2871.0</td>
        </tr>
        <tr>
            <td>Wadley Regional Medical Center</td>
            <td>Texarkana</td>
            <td>TX</td>
            <td>2872.0</td>
        </tr>
        <tr>
            <td>Russell Medical Center</td>
            <td>Alexander City</td>
            <td>AL</td>
            <td>2873.0</td>
        </tr>
        <tr>
            <td>Cookeville Regional Medical Center</td>
            <td>Cookeville</td>
            <td>TN</td>
            <td>2874.0</td>
        </tr>
        <tr>
            <td>Penn Highlands Dubois</td>
            <td>Dubois</td>
            <td>PA</td>
            <td>2875.0</td>
        </tr>
        <tr>
            <td>Lutheran Hospital of Indiana</td>
            <td>Fort Wayne</td>
            <td>IN</td>
            <td>2876.0</td>
        </tr>
        <tr>
            <td>FHN Memorial Hospital</td>
            <td>Freeport</td>
            <td>IL</td>
            <td>2877.0</td>
        </tr>
        <tr>
            <td>South Baldwin Regional Medical Center</td>
            <td>Foley</td>
            <td>AL</td>
            <td>2878.0</td>
        </tr>
        <tr>
            <td>Wadley Regional Medical Center at Hope</td>
            <td>Hope</td>
            <td>AR</td>
            <td>2879.0</td>
        </tr>
        <tr>
            <td>Henry Ford Macomb Hospital</td>
            <td>Clinton Township</td>
            <td>MI</td>
            <td>2880.0</td>
        </tr>
        <tr>
            <td>Gadsden Regional Medical Center</td>
            <td>Gadsden</td>
            <td>AL</td>
            <td>2881.0</td>
        </tr>
        <tr>
            <td>Corning Hospital</td>
            <td>Corning</td>
            <td>NY</td>
            <td>2882.0</td>
        </tr>
        <tr>
            <td>St. Dominic-Jackson Memorial Hospital</td>
            <td>Jackson</td>
            <td>MS</td>
            <td>2883.0</td>
        </tr>
        <tr>
            <td>Southeastern Ohio Regional Medical Center</td>
            <td>Cambridge</td>
            <td>OH</td>
            <td>2884.0</td>
        </tr>
        <tr>
            <td>Jones Memorial Hospital</td>
            <td>Wellsville</td>
            <td>NY</td>
            <td>2885.0</td>
        </tr>
        <tr>
            <td>Van Wert County Hospital</td>
            <td>Van Wert</td>
            <td>OH</td>
            <td>2886.0</td>
        </tr>
        <tr>
            <td>Baptist Health Floyd</td>
            <td>New Albany</td>
            <td>IN</td>
            <td>2887.0</td>
        </tr>
        <tr>
            <td>Hillcrest Hospital Claremore</td>
            <td>Claremore</td>
            <td>OK</td>
            <td>2888.0</td>
        </tr>
        <tr>
            <td>Doctors Memorial Hospital</td>
            <td>Perry</td>
            <td>FL</td>
            <td>2889.0</td>
        </tr>
        <tr>
            <td>Penn Highlands Brookville</td>
            <td>Brookville</td>
            <td>PA</td>
            <td>2890.0</td>
        </tr>
        <tr>
            <td>Waterbury Hospital</td>
            <td>Waterbury</td>
            <td>CT</td>
            <td>2891.0</td>
        </tr>
        <tr>
            <td>White River Medical Center</td>
            <td>Batesville</td>
            <td>AR</td>
            <td>2892.0</td>
        </tr>
        <tr>
            <td>Rooks County Health Center</td>
            <td>Plainville</td>
            <td>KS</td>
            <td>2893.0</td>
        </tr>
        <tr>
            <td>Flowers Hospital</td>
            <td>Dothan</td>
            <td>AL</td>
            <td>2894.0</td>
        </tr>
        <tr>
            <td>Union General Hospital</td>
            <td>Blairsville</td>
            <td>GA</td>
            <td>2895.0</td>
        </tr>
        <tr>
            <td>Knoxville Hospital &amp; Clinics</td>
            <td>Knoxville</td>
            <td>IA</td>
            <td>2896.0</td>
        </tr>
        <tr>
            <td>Bluffton Regional Medical Center</td>
            <td>Bluffton</td>
            <td>IN</td>
            <td>2897.0</td>
        </tr>
        <tr>
            <td>Santa Rosa Medical Center</td>
            <td>Milton</td>
            <td>FL</td>
            <td>2898.0</td>
        </tr>
        <tr>
            <td>Illinois Valley Community Hospital</td>
            <td>Peru</td>
            <td>IL</td>
            <td>2899.0</td>
        </tr>
        <tr>
            <td>Chan Soon- Shiong Medical Center at Windber</td>
            <td>Windber</td>
            <td>PA</td>
            <td>2900.0</td>
        </tr>
        <tr>
            <td>Henderson Hospital</td>
            <td>Henderson</td>
            <td>NV</td>
            <td>2901.0</td>
        </tr>
        <tr>
            <td>Northwest Hospital Center</td>
            <td>Randallstown</td>
            <td>MD</td>
            <td>2902.0</td>
        </tr>
        <tr>
            <td>Highland District Hospital</td>
            <td>Hillsboro</td>
            <td>OH</td>
            <td>2903.0</td>
        </tr>
        <tr>
            <td>Springhill Memorial Hospital</td>
            <td>Mobile</td>
            <td>AL</td>
            <td>2904.0</td>
        </tr>
        <tr>
            <td>Bayfront Health Port Charlotte</td>
            <td>Port Charlotte</td>
            <td>FL</td>
            <td>2905.0</td>
        </tr>
        <tr>
            <td>Butler County Health Care Center</td>
            <td>David City</td>
            <td>NE</td>
            <td>2906.0</td>
        </tr>
        <tr>
            <td>Penn Highlands Clearfield</td>
            <td>Clearfield</td>
            <td>PA</td>
            <td>2907.0</td>
        </tr>
        <tr>
            <td>Wellington Regional Medical Center</td>
            <td>Wellington</td>
            <td>FL</td>
            <td>2909.0</td>
        </tr>
        <tr>
            <td>Leesburg Regional Medical Center</td>
            <td>Leesburg</td>
            <td>FL</td>
            <td>2910.0</td>
        </tr>
        <tr>
            <td>Witham Health Services</td>
            <td>Lebanon</td>
            <td>IN</td>
            <td>2911.0</td>
        </tr>
        <tr>
            <td>Terrebonne General Medical Center</td>
            <td>Houma</td>
            <td>LA</td>
            <td>2912.0</td>
        </tr>
        <tr>
            <td>Mt. Graham Regional Medical Center</td>
            <td>Safford</td>
            <td>AZ</td>
            <td>2913.0</td>
        </tr>
        <tr>
            <td>Mease Countryside Hospital</td>
            <td>Safety Harbor</td>
            <td>FL</td>
            <td>2914.0</td>
        </tr>
        <tr>
            <td>Dekalb Regional Medical Center</td>
            <td>Fort Payne</td>
            <td>AL</td>
            <td>2915.0</td>
        </tr>
        <tr>
            <td>Och Regional Medical Center</td>
            <td>Starkville</td>
            <td>MS</td>
            <td>2916.0</td>
        </tr>
        <tr>
            <td>McLaren Lapeer Region</td>
            <td>Lapeer</td>
            <td>MI</td>
            <td>2917.0</td>
        </tr>
        <tr>
            <td>Waverly Health Center</td>
            <td>Waverly</td>
            <td>IA</td>
            <td>2918.0</td>
        </tr>
        <tr>
            <td>UT Health East Texas Tyler Regional Hospital</td>
            <td>Tyler</td>
            <td>TX</td>
            <td>2919.0</td>
        </tr>
        <tr>
            <td>Jackson General Hospital</td>
            <td>Ripley</td>
            <td>WV</td>
            <td>2920.0</td>
        </tr>
        <tr>
            <td>The Medical Center of Southeast Texas</td>
            <td>Port Arthur</td>
            <td>TX</td>
            <td>2921.0</td>
        </tr>
        <tr>
            <td>Dale Medical Center</td>
            <td>Ozark</td>
            <td>AL</td>
            <td>2922.0</td>
        </tr>
        <tr>
            <td>Longview Regional Medical Center</td>
            <td>Longview</td>
            <td>TX</td>
            <td>2923.0</td>
        </tr>
        <tr>
            <td>Tyler Memorial Hospital</td>
            <td>Tunkhannock</td>
            <td>PA</td>
            <td>2924.0</td>
        </tr>
        <tr>
            <td>Broward Health North</td>
            <td>Pompano Beach</td>
            <td>FL</td>
            <td>2925.0</td>
        </tr>
        <tr>
            <td>Liberty Hospital</td>
            <td>Liberty</td>
            <td>MO</td>
            <td>2926.0</td>
        </tr>
        <tr>
            <td>Kosciusko Community Hospital</td>
            <td>Warsaw</td>
            <td>IN</td>
            <td>2927.0</td>
        </tr>
        <tr>
            <td>Aurora Medical Center Burlington</td>
            <td>Burlington</td>
            <td>WI</td>
            <td>2928.0</td>
        </tr>
        <tr>
            <td>Cass Regional Medical Center</td>
            <td>Harrisonville</td>
            <td>MO</td>
            <td>2929.0</td>
        </tr>
        <tr>
            <td>Valley View Medical Center</td>
            <td>Fort Mohave</td>
            <td>AZ</td>
            <td>2930.0</td>
        </tr>
        <tr>
            <td>Sovah Health Danville</td>
            <td>Danville</td>
            <td>VA</td>
            <td>2931.0</td>
        </tr>
        <tr>
            <td>Liberty Regional Medical Center</td>
            <td>Hinesville</td>
            <td>GA</td>
            <td>2932.0</td>
        </tr>
        <tr>
            <td>Baptist Medical Center East</td>
            <td>Montgomery</td>
            <td>AL</td>
            <td>2933.0</td>
        </tr>
        <tr>
            <td>Broward Health Coral Springs</td>
            <td>Coral Springs</td>
            <td>FL</td>
            <td>2934.0</td>
        </tr>
        <tr>
            <td>Cape Fear Valley-Bladen County Hospital</td>
            <td>Elizabethtown</td>
            <td>NC</td>
            <td>2935.0</td>
        </tr>
        <tr>
            <td>Middlesboro Appalachian Regional Healthcare Hospital</td>
            <td>Middlesboro</td>
            <td>KY</td>
            <td>2936.0</td>
        </tr>
        <tr>
            <td>Broward Health Medical Center</td>
            <td>Fort Lauderdale</td>
            <td>FL</td>
            <td>2937.0</td>
        </tr>
        <tr>
            <td>Good Samaritan Hospital</td>
            <td>Vincennes</td>
            <td>IN</td>
            <td>2938.0</td>
        </tr>
        <tr>
            <td>Bayfront Health Punta Gorda</td>
            <td>Punta Gorda</td>
            <td>FL</td>
            <td>2939.0</td>
        </tr>
        <tr>
            <td>Ste Genevieve County Memorial Hospital</td>
            <td>Sainte Genevieve</td>
            <td>MO</td>
            <td>2940.0</td>
        </tr>
        <tr>
            <td>Hugh Chatham Memorial Hospital</td>
            <td>Elkin</td>
            <td>NC</td>
            <td>2941.0</td>
        </tr>
        <tr>
            <td>Cameron Memorial Community Hospital</td>
            <td>Angola</td>
            <td>IN</td>
            <td>2942.0</td>
        </tr>
        <tr>
            <td>Bon Secours Hospital</td>
            <td>Baltimore</td>
            <td>MD</td>
            <td>2943.0</td>
        </tr>
        <tr>
            <td>Fannin Regional Hospital</td>
            <td>Blue Ridge</td>
            <td>GA</td>
            <td>2944.0</td>
        </tr>
        <tr>
            <td>Wilkes-Barre General Hospital</td>
            <td>Wilkes-Barre</td>
            <td>PA</td>
            <td>2945.0</td>
        </tr>
        <tr>
            <td>Poplar Bluff Regional Medical Center</td>
            <td>Poplar Bluff</td>
            <td>MO</td>
            <td>2946.0</td>
        </tr>
        <tr>
            <td>Aspirus Iron River Hospital &amp; Clinics</td>
            <td>Iron River</td>
            <td>MI</td>
            <td>2947.0</td>
        </tr>
        <tr>
            <td>Jersey Community Hospital</td>
            <td>Jerseyville</td>
            <td>IL</td>
            <td>2948.0</td>
        </tr>
        <tr>
            <td>Yoakum Community Hospital</td>
            <td>Yoakum</td>
            <td>TX</td>
            <td>2949.0</td>
        </tr>
        <tr>
            <td>Big Bend Regional Medical Center</td>
            <td>Alpine</td>
            <td>TX</td>
            <td>2950.0</td>
        </tr>
        <tr>
            <td>Wickenburg Community Hospital</td>
            <td>Wickenburg</td>
            <td>AZ</td>
            <td>2951.0</td>
        </tr>
        <tr>
            <td>Grove City Medical Center</td>
            <td>Grove City</td>
            <td>PA</td>
            <td>2952.0</td>
        </tr>
        <tr>
            <td>Whittier Hospital Medical Center</td>
            <td>Whittier</td>
            <td>CA</td>
            <td>2953.0</td>
        </tr>
        <tr>
            <td>Cullman Regional Medical Center</td>
            <td>Cullman</td>
            <td>AL</td>
            <td>2954.0</td>
        </tr>
        <tr>
            <td>Warren General Hospital</td>
            <td>Warren</td>
            <td>PA</td>
            <td>2955.0</td>
        </tr>
        <tr>
            <td>Ringgold County Hospital</td>
            <td>Mount Ayr</td>
            <td>IA</td>
            <td>2956.0</td>
        </tr>
        <tr>
            <td>Johnson County Hospital</td>
            <td>Tecumseh</td>
            <td>NE</td>
            <td>2957.0</td>
        </tr>
        <tr>
            <td>Acadia General Hospital</td>
            <td>Crowley</td>
            <td>LA</td>
            <td>2958.0</td>
        </tr>
        <tr>
            <td>Mariners Hospital</td>
            <td>Tavernier</td>
            <td>FL</td>
            <td>2959.0</td>
        </tr>
        <tr>
            <td>MUSC Health Chester Medical Center</td>
            <td>Chester</td>
            <td>SC</td>
            <td>2960.0</td>
        </tr>
        <tr>
            <td>Habersham County Medical Center</td>
            <td>Demorest</td>
            <td>GA</td>
            <td>2961.0</td>
        </tr>
        <tr>
            <td>Washington County Hospital and Clinics</td>
            <td>Washington</td>
            <td>IA</td>
            <td>2962.0</td>
        </tr>
        <tr>
            <td>University of Texas Health Science Center at Tyler</td>
            <td>Tyler</td>
            <td>TX</td>
            <td>2963.0</td>
        </tr>
        <tr>
            <td>Guttenberg Municipal Hospital</td>
            <td>Guttenberg</td>
            <td>IA</td>
            <td>2965.0</td>
        </tr>
        <tr>
            <td>Starr Regional Medical Center Athens</td>
            <td>Athens</td>
            <td>TN</td>
            <td>2966.0</td>
        </tr>
        <tr>
            <td>Merit Health Rankin</td>
            <td>Brandon</td>
            <td>MS</td>
            <td>2967.0</td>
        </tr>
        <tr>
            <td>Meade District Hospital</td>
            <td>Meade</td>
            <td>KS</td>
            <td>2968.0</td>
        </tr>
        <tr>
            <td>Plateau Medical Center</td>
            <td>Oak Hill</td>
            <td>WV</td>
            <td>2969.0</td>
        </tr>
        <tr>
            <td>Goodall Witcher Hospital</td>
            <td>Clifton</td>
            <td>TX</td>
            <td>2970.0</td>
        </tr>
        <tr>
            <td>King&#x27;s Daughters&#x27; Health</td>
            <td>Madison</td>
            <td>IN</td>
            <td>2971.0</td>
        </tr>
        <tr>
            <td>Hillcrest Hospital Pryor</td>
            <td>Pryor</td>
            <td>OK</td>
            <td>2972.0</td>
        </tr>
        <tr>
            <td>Crawford County Memorial Hospital</td>
            <td>Denison</td>
            <td>IA</td>
            <td>2973.0</td>
        </tr>
        <tr>
            <td>Gateway Regional Medical Center</td>
            <td>Granite City</td>
            <td>IL</td>
            <td>2974.0</td>
        </tr>
        <tr>
            <td>L V Stabler Memorial Hospital</td>
            <td>Greenville</td>
            <td>AL</td>
            <td>2975.0</td>
        </tr>
        <tr>
            <td>Princeton Community Hospital</td>
            <td>Princeton</td>
            <td>WV</td>
            <td>2976.0</td>
        </tr>
        <tr>
            <td>Anderson Hospital</td>
            <td>Maryville</td>
            <td>IL</td>
            <td>2977.0</td>
        </tr>
        <tr>
            <td>Daviess Community Hospital</td>
            <td>Washington</td>
            <td>IN</td>
            <td>2978.0</td>
        </tr>
        <tr>
            <td>Crete Area Medical Center</td>
            <td>Crete</td>
            <td>NE</td>
            <td>2979.0</td>
        </tr>
        <tr>
            <td>Davis County Hospital</td>
            <td>Bloomfield</td>
            <td>IA</td>
            <td>2981.0</td>
        </tr>
        <tr>
            <td>Community Memorial Hospital Medical Center</td>
            <td>Sumner</td>
            <td>IA</td>
            <td>2982.0</td>
        </tr>
        <tr>
            <td>Medical Center Enterprise</td>
            <td>Enterprise</td>
            <td>AL</td>
            <td>2983.0</td>
        </tr>
        <tr>
            <td>Ozark Health</td>
            <td>Clinton</td>
            <td>AR</td>
            <td>2984.0</td>
        </tr>
        <tr>
            <td>King&#x27;s Daughters Medical Center-Brookhaven</td>
            <td>Brookhaven</td>
            <td>MS</td>
            <td>2985.0</td>
        </tr>
        <tr>
            <td>Garrison Memorial Hospital</td>
            <td>Garrison</td>
            <td>ND</td>
            <td>2986.0</td>
        </tr>
        <tr>
            <td>Spring View Hospital</td>
            <td>Lebanon</td>
            <td>KY</td>
            <td>2987.0</td>
        </tr>
        <tr>
            <td>Lakewood Ranch Medical Center</td>
            <td>Bradenton</td>
            <td>FL</td>
            <td>2988.0</td>
        </tr>
        <tr>
            <td>Huntsville Hospital</td>
            <td>Huntsville</td>
            <td>AL</td>
            <td>2989.0</td>
        </tr>
        <tr>
            <td>Kearney Regional Medical Center</td>
            <td>Kearney</td>
            <td>NE</td>
            <td>2990.0</td>
        </tr>
        <tr>
            <td>MidMichigan Medical Center-Midland</td>
            <td>Midland</td>
            <td>MI</td>
            <td>2991.0</td>
        </tr>
        <tr>
            <td>Baptist Health Louisville</td>
            <td>Louisville</td>
            <td>KY</td>
            <td>2992.0</td>
        </tr>
        <tr>
            <td>Saint Rose Dominican Hospitals - Siena Campus</td>
            <td>Henderson</td>
            <td>NV</td>
            <td>2994.0</td>
        </tr>
        <tr>
            <td>Henry Mayo NewhallÂ¬â€  Hospital</td>
            <td>Valencia</td>
            <td>CA</td>
            <td>2995.0</td>
        </tr>
        <tr>
            <td>Holy Redeemer Hospital and Medical Center</td>
            <td>Meadowbrook</td>
            <td>PA</td>
            <td>2996.0</td>
        </tr>
        <tr>
            <td>Hancock Regional Hospital</td>
            <td>Greenfield</td>
            <td>IN</td>
            <td>2997.0</td>
        </tr>
        <tr>
            <td>Hillsdale Hospital</td>
            <td>Hillsdale</td>
            <td>MI</td>
            <td>2998.0</td>
        </tr>
        <tr>
            <td>Castleview Hospital</td>
            <td>Price</td>
            <td>UT</td>
            <td>2999.0</td>
        </tr>
        <tr>
            <td>Adams Memorial Hospital</td>
            <td>Decatur</td>
            <td>IN</td>
            <td>3000.0</td>
        </tr>
        <tr>
            <td>Ivinson Memorial Hospital</td>
            <td>Laramie</td>
            <td>WY</td>
            <td>3001.0</td>
        </tr>
        <tr>
            <td>Atmore Community Hospital</td>
            <td>Atmore</td>
            <td>AL</td>
            <td>3002.0</td>
        </tr>
        <tr>
            <td>Dodge County Hospital</td>
            <td>Eastman</td>
            <td>GA</td>
            <td>3003.0</td>
        </tr>
        <tr>
            <td>Hudson Regional Hospital</td>
            <td>Secaucus</td>
            <td>NJ</td>
            <td>3004.0</td>
        </tr>
        <tr>
            <td>Baptist Emergency Hospital</td>
            <td>San Antonio</td>
            <td>TX</td>
            <td>3005.0</td>
        </tr>
        <tr>
            <td>Mercy Regional Medical Center</td>
            <td>Ville Platte</td>
            <td>LA</td>
            <td>3006.0</td>
        </tr>
        <tr>
            <td>SSM Health St. Anthony Hospital - Oklahoma City</td>
            <td>Oklahoma City</td>
            <td>OK</td>
            <td>3007.0</td>
        </tr>
        <tr>
            <td>Aurora St. Lukes Medical Center</td>
            <td>Milwaukee</td>
            <td>WI</td>
            <td>3008.0</td>
        </tr>
        <tr>
            <td>Vidant Medical Center</td>
            <td>Greenville</td>
            <td>NC</td>
            <td>3009.0</td>
        </tr>
        <tr>
            <td>Mclaren Greater Lansing</td>
            <td>Lansing</td>
            <td>MI</td>
            <td>3010.0</td>
        </tr>
        <tr>
            <td>Lehigh Valley Hospital-Schuylkill S. Jackson Street</td>
            <td>Pottsville</td>
            <td>PA</td>
            <td>3011.0</td>
        </tr>
        <tr>
            <td>Clark Regional Medical Center</td>
            <td>Winchester</td>
            <td>KY</td>
            <td>3012.0</td>
        </tr>
        <tr>
            <td>Clovis Community Medical Center</td>
            <td>Clovis</td>
            <td>CA</td>
            <td>3013.0</td>
        </tr>
        <tr>
            <td>Gettysburg Hospital</td>
            <td>Gettysburg</td>
            <td>PA</td>
            <td>3014.0</td>
        </tr>
        <tr>
            <td>Plantation General Hospital</td>
            <td>Plantation</td>
            <td>FL</td>
            <td>3015.0</td>
        </tr>
        <tr>
            <td>Carris Health</td>
            <td>Willmar</td>
            <td>MN</td>
            <td>3016.0</td>
        </tr>
        <tr>
            <td>St. Vincent&#x27;s Medical Center</td>
            <td>Bridgeport</td>
            <td>CT</td>
            <td>3017.0</td>
        </tr>
        <tr>
            <td>Great River Medical Center</td>
            <td>West Burlington</td>
            <td>IA</td>
            <td>3018.0</td>
        </tr>
        <tr>
            <td>Piedmont Mountainside Hospital</td>
            <td>Jasper</td>
            <td>GA</td>
            <td>3019.0</td>
        </tr>
        <tr>
            <td>The Hospitals Of Providence - East Campus</td>
            <td>El Paso</td>
            <td>TX</td>
            <td>3020.0</td>
        </tr>
        <tr>
            <td>Franciscan Health Michigan City</td>
            <td>Michigan City</td>
            <td>IN</td>
            <td>3021.0</td>
        </tr>
        <tr>
            <td>Phelps Health</td>
            <td>Rolla</td>
            <td>MO</td>
            <td>3022.0</td>
        </tr>
        <tr>
            <td>Pottstown Hospital</td>
            <td>Pottstown</td>
            <td>PA</td>
            <td>3023.0</td>
        </tr>
        <tr>
            <td>Mary Imogene Bassett Hospital</td>
            <td>Cooperstown</td>
            <td>NY</td>
            <td>3024.0</td>
        </tr>
        <tr>
            <td>Columbia Memorial Hospital</td>
            <td>Hudson</td>
            <td>NY</td>
            <td>3025.0</td>
        </tr>
        <tr>
            <td>Lakeland Regional Medical Center</td>
            <td>Lakeland</td>
            <td>FL</td>
            <td>3026.0</td>
        </tr>
        <tr>
            <td>Merit Health Biloxi</td>
            <td>Biloxi</td>
            <td>MS</td>
            <td>3027.0</td>
        </tr>
        <tr>
            <td>Jackson-Madison County General Hospital</td>
            <td>Jackson</td>
            <td>TN</td>
            <td>3028.0</td>
        </tr>
        <tr>
            <td>Christus Southeast Texas - St. Elizabeth</td>
            <td>Beaumont</td>
            <td>TX</td>
            <td>3029.0</td>
        </tr>
        <tr>
            <td>Trinity Medical Center East &amp; Trinity Medical Center West</td>
            <td>Steubenville</td>
            <td>OH</td>
            <td>3030.0</td>
        </tr>
        <tr>
            <td>Phoenixville Hospital</td>
            <td>Phoenixville</td>
            <td>PA</td>
            <td>3031.0</td>
        </tr>
        <tr>
            <td>Robert Wood Johnson University Hospital</td>
            <td>New Brunswick</td>
            <td>NJ</td>
            <td>3033.0</td>
        </tr>
        <tr>
            <td>Mclaren Flint</td>
            <td>Flint</td>
            <td>MI</td>
            <td>3034.0</td>
        </tr>
        <tr>
            <td>Paris Regional Medical Center</td>
            <td>Paris</td>
            <td>TX</td>
            <td>3035.0</td>
        </tr>
        <tr>
            <td>Tennova Healthcare-Clarksville</td>
            <td>Clarksville</td>
            <td>TN</td>
            <td>3036.0</td>
        </tr>
        <tr>
            <td>Dameron Hospital</td>
            <td>Stockton</td>
            <td>CA</td>
            <td>3037.0</td>
        </tr>
        <tr>
            <td>Jackson Hospital &amp; Clinic</td>
            <td>Montgomery</td>
            <td>AL</td>
            <td>3038.0</td>
        </tr>
        <tr>
            <td>Northwest Mississippi Medical Center</td>
            <td>Clarksdale</td>
            <td>MS</td>
            <td>3039.0</td>
        </tr>
        <tr>
            <td>Citrus Memorial Hospital</td>
            <td>Inverness</td>
            <td>FL</td>
            <td>3040.0</td>
        </tr>
        <tr>
            <td>La Porte Hospital</td>
            <td>La Porte</td>
            <td>IN</td>
            <td>3041.0</td>
        </tr>
        <tr>
            <td>Nash General Hospital</td>
            <td>Rocky Mount</td>
            <td>NC</td>
            <td>3042.0</td>
        </tr>
        <tr>
            <td>Willis Knighton Medical Center</td>
            <td>Shreveport</td>
            <td>LA</td>
            <td>3044.0</td>
        </tr>
        <tr>
            <td>MidMichigan Medical Center - Alpena</td>
            <td>Alpena</td>
            <td>MI</td>
            <td>3045.0</td>
        </tr>
        <tr>
            <td>Meadows Regional Medical Center</td>
            <td>Vidalia</td>
            <td>GA</td>
            <td>3046.0</td>
        </tr>
        <tr>
            <td>Southeastern Regional Medical Center</td>
            <td>Lumberton</td>
            <td>NC</td>
            <td>3047.0</td>
        </tr>
        <tr>
            <td>Anna Jaques Hospital</td>
            <td>Newburyport</td>
            <td>MA</td>
            <td>3048.0</td>
        </tr>
        <tr>
            <td>Harrington Memorial Hospital</td>
            <td>Southbridge</td>
            <td>MA</td>
            <td>3049.0</td>
        </tr>
        <tr>
            <td>Bayfront Health - St. Petersburg</td>
            <td>Saint Petersburg</td>
            <td>FL</td>
            <td>3050.0</td>
        </tr>
        <tr>
            <td>Northwest Medical Center</td>
            <td>Margate</td>
            <td>FL</td>
            <td>3051.0</td>
        </tr>
        <tr>
            <td>Saint Rose Dominican Hospitals - San Martin Campus</td>
            <td>Las Vegas</td>
            <td>NV</td>
            <td>3053.0</td>
        </tr>
        <tr>
            <td>Southampton Memorial Hospital</td>
            <td>Franklin</td>
            <td>VA</td>
            <td>3054.0</td>
        </tr>
        <tr>
            <td>Pioneers Memorial Healthcare District</td>
            <td>Brawley</td>
            <td>CA</td>
            <td>3055.0</td>
        </tr>
        <tr>
            <td>McLeod Health Cheraw</td>
            <td>Cheraw</td>
            <td>SC</td>
            <td>3056.0</td>
        </tr>
        <tr>
            <td>Carroll Hospital Center</td>
            <td>Westminster</td>
            <td>MD</td>
            <td>3057.0</td>
        </tr>
        <tr>
            <td>Richmond University Medical Center</td>
            <td>Staten Island</td>
            <td>NY</td>
            <td>3058.0</td>
        </tr>
        <tr>
            <td>Shore Medical Center</td>
            <td>Somers Point</td>
            <td>NJ</td>
            <td>3059.0</td>
        </tr>
        <tr>
            <td>Bayfront Health Seven Rivers</td>
            <td>Crystal River</td>
            <td>FL</td>
            <td>3060.0</td>
        </tr>
        <tr>
            <td>CHRISTUS Spohn Hospital Corpus Christi</td>
            <td>Corpus Christi</td>
            <td>TX</td>
            <td>3061.0</td>
        </tr>
        <tr>
            <td>NorthCrest Medical Center</td>
            <td>Springfield</td>
            <td>TN</td>
            <td>3062.0</td>
        </tr>
        <tr>
            <td>Riverview Regional Medical Center</td>
            <td>Gadsden</td>
            <td>AL</td>
            <td>3063.0</td>
        </tr>
        <tr>
            <td>Providence Saint Joseph Medical Center</td>
            <td>Burbank</td>
            <td>CA</td>
            <td>3064.0</td>
        </tr>
        <tr>
            <td>Canton-Potsdam Hospital</td>
            <td>Potsdam</td>
            <td>NY</td>
            <td>3065.0</td>
        </tr>
        <tr>
            <td>Jefferson Regional Medical Center</td>
            <td>Pine Bluff</td>
            <td>AR</td>
            <td>3066.0</td>
        </tr>
        <tr>
            <td>Riverview Health</td>
            <td>Noblesville</td>
            <td>IN</td>
            <td>3067.0</td>
        </tr>
        <tr>
            <td>Baptist Medical Center South</td>
            <td>Montgomery</td>
            <td>AL</td>
            <td>3068.0</td>
        </tr>
        <tr>
            <td>Barstow Community Hospital</td>
            <td>Barstow</td>
            <td>CA</td>
            <td>3069.0</td>
        </tr>
        <tr>
            <td>Doctors Hospital of Manteca</td>
            <td>Manteca</td>
            <td>CA</td>
            <td>3070.0</td>
        </tr>
        <tr>
            <td>Crisp Regional Hospital</td>
            <td>Cordele</td>
            <td>GA</td>
            <td>3071.0</td>
        </tr>
        <tr>
            <td>Murray-Calloway County Hospital</td>
            <td>Murray</td>
            <td>KY</td>
            <td>3072.0</td>
        </tr>
        <tr>
            <td>Los Alamitos Medical Center</td>
            <td>Los Alamitos</td>
            <td>CA</td>
            <td>3073.0</td>
        </tr>
        <tr>
            <td>Monterey Park Hospital</td>
            <td>Monterey Park</td>
            <td>CA</td>
            <td>3074.0</td>
        </tr>
        <tr>
            <td>Doctors Hospital at Renaissance</td>
            <td>Edinburg</td>
            <td>TX</td>
            <td>3075.0</td>
        </tr>
        <tr>
            <td>Parrish Medical Center</td>
            <td>Titusville</td>
            <td>FL</td>
            <td>3076.0</td>
        </tr>
        <tr>
            <td>Northern Louisiana Medical Center</td>
            <td>Ruston</td>
            <td>LA</td>
            <td>3077.0</td>
        </tr>
        <tr>
            <td>Virtua Willingboro Hospital</td>
            <td>Willingboro</td>
            <td>NJ</td>
            <td>3078.0</td>
        </tr>
        <tr>
            <td>Andalusia Health</td>
            <td>Andalusia</td>
            <td>AL</td>
            <td>3079.0</td>
        </tr>
        <tr>
            <td>Crittenden Health System</td>
            <td>Marion</td>
            <td>KY</td>
            <td>3080.0</td>
        </tr>
        <tr>
            <td>Trinitas Regional Medical Center</td>
            <td>Elizabeth</td>
            <td>NJ</td>
            <td>3081.0</td>
        </tr>
        <tr>
            <td>Integris Health Edmond</td>
            <td>Edmond</td>
            <td>OK</td>
            <td>3082.0</td>
        </tr>
        <tr>
            <td>Carolinas Hospital System Marion</td>
            <td>Mullins</td>
            <td>SC</td>
            <td>3083.0</td>
        </tr>
        <tr>
            <td>Brodstone Memorial Hospital</td>
            <td>Superior</td>
            <td>NE</td>
            <td>3084.0</td>
        </tr>
        <tr>
            <td>Columbus Regional Healthcare System</td>
            <td>Whiteville</td>
            <td>NC</td>
            <td>3085.0</td>
        </tr>
        <tr>
            <td>Orange County Global Medical Center</td>
            <td>Santa Ana</td>
            <td>CA</td>
            <td>3086.0</td>
        </tr>
        <tr>
            <td>Pikeville Medical Center</td>
            <td>Pikeville</td>
            <td>KY</td>
            <td>3087.0</td>
        </tr>
        <tr>
            <td>Cary Medical Center</td>
            <td>Caribou</td>
            <td>ME</td>
            <td>3088.0</td>
        </tr>
        <tr>
            <td>West Kendall Baptist Hospital</td>
            <td>Miami</td>
            <td>FL</td>
            <td>3089.0</td>
        </tr>
        <tr>
            <td>Copley Hospital</td>
            <td>Morrisville</td>
            <td>VT</td>
            <td>3090.0</td>
        </tr>
        <tr>
            <td>SoutheastHEALTH</td>
            <td>Cape Girardeau</td>
            <td>MO</td>
            <td>3091.0</td>
        </tr>
        <tr>
            <td>Charleston Area Medical Center</td>
            <td>Charleston</td>
            <td>WV</td>
            <td>3092.0</td>
        </tr>
        <tr>
            <td>Glacial Ridge Hospital</td>
            <td>Glenwood</td>
            <td>MN</td>
            <td>3093.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital of Carbon County</td>
            <td>Rawlins</td>
            <td>WY</td>
            <td>3094.0</td>
        </tr>
        <tr>
            <td>San Gorgonio Memorial Hospital</td>
            <td>Banning</td>
            <td>CA</td>
            <td>3095.0</td>
        </tr>
        <tr>
            <td>Highlands Medical Center</td>
            <td>Scottsboro</td>
            <td>AL</td>
            <td>3096.0</td>
        </tr>
        <tr>
            <td>Claxton-Hepburn Medical Center</td>
            <td>Ogdensburg</td>
            <td>NY</td>
            <td>3097.0</td>
        </tr>
        <tr>
            <td>Homestead Hospital</td>
            <td>Homestead</td>
            <td>FL</td>
            <td>3098.0</td>
        </tr>
        <tr>
            <td>Beaumont Hospital - Taylor</td>
            <td>Taylor</td>
            <td>MI</td>
            <td>3099.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital and Health Care Center</td>
            <td>Jasper</td>
            <td>IN</td>
            <td>3100.0</td>
        </tr>
        <tr>
            <td>Great Plains Regional Medical Center</td>
            <td>Elk City</td>
            <td>OK</td>
            <td>3101.0</td>
        </tr>
        <tr>
            <td>The Cooley Dickinson Hospital</td>
            <td>Northampton</td>
            <td>MA</td>
            <td>3102.0</td>
        </tr>
        <tr>
            <td>Halifax Regional Medical Center</td>
            <td>Roanoke Rapids</td>
            <td>NC</td>
            <td>3103.0</td>
        </tr>
        <tr>
            <td>Centracare Health System - Melrose Hospital</td>
            <td>Melrose</td>
            <td>MN</td>
            <td>3104.0</td>
        </tr>
        <tr>
            <td>Ashe Memorial Hospital</td>
            <td>Jefferson</td>
            <td>NC</td>
            <td>3105.0</td>
        </tr>
        <tr>
            <td>Avera St. Anthony&#x27;s Hospital</td>
            <td>O&#x27; Neill</td>
            <td>NE</td>
            <td>3106.0</td>
        </tr>
        <tr>
            <td>Wheeling Hospital</td>
            <td>Wheeling</td>
            <td>WV</td>
            <td>3107.0</td>
        </tr>
        <tr>
            <td>Central Valley Medical Center</td>
            <td>Nephi</td>
            <td>UT</td>
            <td>3108.0</td>
        </tr>
        <tr>
            <td>Parkview Community Hospital Medical Center</td>
            <td>Riverside</td>
            <td>CA</td>
            <td>3109.0</td>
        </tr>
        <tr>
            <td>Coral Gables Hospital</td>
            <td>Coral Gables</td>
            <td>FL</td>
            <td>3110.0</td>
        </tr>
        <tr>
            <td>Mt. San Rafael Hospital</td>
            <td>Trinidad</td>
            <td>CO</td>
            <td>3111.0</td>
        </tr>
        <tr>
            <td>Harlan ARH Hospital</td>
            <td>Harlan</td>
            <td>KY</td>
            <td>3112.0</td>
        </tr>
        <tr>
            <td>Aspirus Ironwood Hospital</td>
            <td>Ironwood</td>
            <td>MI</td>
            <td>3113.0</td>
        </tr>
        <tr>
            <td>Greenwood Leflore Hospital</td>
            <td>Greenwood</td>
            <td>MS</td>
            <td>3114.0</td>
        </tr>
        <tr>
            <td>Citizens Medical Center</td>
            <td>Colby</td>
            <td>KS</td>
            <td>3115.0</td>
        </tr>
        <tr>
            <td>Livingston Regional Hospital</td>
            <td>Livingston</td>
            <td>TN</td>
            <td>3116.0</td>
        </tr>
        <tr>
            <td>OSF Saint Anthony&#x27;s Health Center</td>
            <td>Alton</td>
            <td>IL</td>
            <td>3117.0</td>
        </tr>
        <tr>
            <td>Northeastern Health System</td>
            <td>Tahlequah</td>
            <td>OK</td>
            <td>3118.0</td>
        </tr>
        <tr>
            <td>Magnolia Hospital</td>
            <td>Magnolia</td>
            <td>AR</td>
            <td>3119.0</td>
        </tr>
        <tr>
            <td>Cherokee Medical Center</td>
            <td>Gaffney</td>
            <td>SC</td>
            <td>3120.0</td>
        </tr>
        <tr>
            <td>Delano Regional Medical Center</td>
            <td>Delano</td>
            <td>CA</td>
            <td>3121.0</td>
        </tr>
        <tr>
            <td>MidMichigan Medical Center-Gladwin</td>
            <td>Gladwin</td>
            <td>MI</td>
            <td>3122.0</td>
        </tr>
        <tr>
            <td>Holy Name Medical Center</td>
            <td>Teaneck</td>
            <td>NJ</td>
            <td>3123.0</td>
        </tr>
        <tr>
            <td>North Logan Mercy Hospital</td>
            <td>Paris</td>
            <td>AR</td>
            <td>3124.0</td>
        </tr>
        <tr>
            <td>Coryell Memorial Healthcare System</td>
            <td>Gatesville</td>
            <td>TX</td>
            <td>3125.0</td>
        </tr>
        <tr>
            <td>Jackson Park Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>3126.0</td>
        </tr>
        <tr>
            <td>Westchester Medical Center</td>
            <td>Valhalla</td>
            <td>NY</td>
            <td>3127.0</td>
        </tr>
        <tr>
            <td>Geary Community Hospital</td>
            <td>Junction City</td>
            <td>KS</td>
            <td>3128.0</td>
        </tr>
        <tr>
            <td>Orange City Area Health System</td>
            <td>Orange City</td>
            <td>IA</td>
            <td>3129.0</td>
        </tr>
        <tr>
            <td>Hale County Hospital</td>
            <td>Greensboro</td>
            <td>AL</td>
            <td>3130.0</td>
        </tr>
        <tr>
            <td>Marlette Regional Hospital</td>
            <td>Marlette</td>
            <td>MI</td>
            <td>3131.0</td>
        </tr>
        <tr>
            <td>Lifecare Medical Center</td>
            <td>Roseau</td>
            <td>MN</td>
            <td>3132.0</td>
        </tr>
        <tr>
            <td>Black River Memorial Hospital</td>
            <td>Black River Falls</td>
            <td>WI</td>
            <td>3133.0</td>
        </tr>
        <tr>
            <td>Edgefield County Healthcare</td>
            <td>Edgefield</td>
            <td>SC</td>
            <td>3134.0</td>
        </tr>
        <tr>
            <td>Van Buren County Hospital</td>
            <td>Keosauqua</td>
            <td>IA</td>
            <td>3135.0</td>
        </tr>
        <tr>
            <td>Allegan General Hospital</td>
            <td>Allegan</td>
            <td>MI</td>
            <td>3136.0</td>
        </tr>
        <tr>
            <td>Healthmark Regional Medical Center</td>
            <td>Defuniak Springs</td>
            <td>FL</td>
            <td>3137.0</td>
        </tr>
        <tr>
            <td>Mille Lacs Health System</td>
            <td>Onamia</td>
            <td>MN</td>
            <td>3138.0</td>
        </tr>
        <tr>
            <td>Burnett Medical Center</td>
            <td>Grantsburg</td>
            <td>WI</td>
            <td>3139.0</td>
        </tr>
        <tr>
            <td>UT Health East Texas Carthage Hospital</td>
            <td>Carthage</td>
            <td>TX</td>
            <td>3140.0</td>
        </tr>
        <tr>
            <td>Community Hospital, Onaga and St. Marys Campus</td>
            <td>Onaga</td>
            <td>KS</td>
            <td>3141.0</td>
        </tr>
        <tr>
            <td>Jeff Davis Hospital</td>
            <td>Hazlehurst</td>
            <td>GA</td>
            <td>3142.0</td>
        </tr>
        <tr>
            <td>Delta Regional Medical Center</td>
            <td>Greenville</td>
            <td>MS</td>
            <td>3143.0</td>
        </tr>
        <tr>
            <td>Anson General Hospital</td>
            <td>Anson</td>
            <td>TX</td>
            <td>3144.0</td>
        </tr>
        <tr>
            <td>Clark Fork Valley Hospital</td>
            <td>Plains</td>
            <td>MT</td>
            <td>3145.0</td>
        </tr>
        <tr>
            <td>National Park Medical Center</td>
            <td>Hot Springs</td>
            <td>AR</td>
            <td>3146.0</td>
        </tr>
        <tr>
            <td>Colorado Canyons Hospital and Medical Center</td>
            <td>Fruita</td>
            <td>CO</td>
            <td>3147.0</td>
        </tr>
        <tr>
            <td>Nemaha Valley Community Hospital</td>
            <td>Seneca</td>
            <td>KS</td>
            <td>3148.0</td>
        </tr>
        <tr>
            <td>Essentia Health Fosston</td>
            <td>Fosston</td>
            <td>MN</td>
            <td>3149.0</td>
        </tr>
        <tr>
            <td>Lindsborg Community Hospital</td>
            <td>Lindsborg</td>
            <td>KS</td>
            <td>3150.0</td>
        </tr>
        <tr>
            <td>Comanche County Medical Center</td>
            <td>Comanche</td>
            <td>TX</td>
            <td>3151.0</td>
        </tr>
        <tr>
            <td>Jennie M Melham Memorial Medical Center</td>
            <td>Broken Bow</td>
            <td>NE</td>
            <td>3152.0</td>
        </tr>
        <tr>
            <td>Crenshaw Community Hospital</td>
            <td>Luverne</td>
            <td>AL</td>
            <td>3153.0</td>
        </tr>
        <tr>
            <td>Bryan W. Whitfield Memorial Hospital</td>
            <td>Demopolis</td>
            <td>AL</td>
            <td>3154.0</td>
        </tr>
        <tr>
            <td>Community Memorial Healthcare</td>
            <td>Marysville</td>
            <td>KS</td>
            <td>3155.0</td>
        </tr>
        <tr>
            <td>Union Hospital Clinton</td>
            <td>Clinton</td>
            <td>IN</td>
            <td>3156.0</td>
        </tr>
        <tr>
            <td>Sweetwater Hospital Association</td>
            <td>Sweetwater</td>
            <td>TN</td>
            <td>3157.0</td>
        </tr>
        <tr>
            <td>Lake Martin Community Hospital</td>
            <td>Dadeville</td>
            <td>AL</td>
            <td>3158.0</td>
        </tr>
        <tr>
            <td>Rush Foundation Hospital</td>
            <td>Meridian</td>
            <td>MS</td>
            <td>3159.0</td>
        </tr>
        <tr>
            <td>La Paz Regional Hospital</td>
            <td>Parker</td>
            <td>AZ</td>
            <td>3160.0</td>
        </tr>
        <tr>
            <td>Lawrence County Memorial Hospital</td>
            <td>Lawrenceville</td>
            <td>IL</td>
            <td>3161.0</td>
        </tr>
        <tr>
            <td>Amberwell Hiawatha</td>
            <td>Hiawatha</td>
            <td>KS</td>
            <td>3162.0</td>
        </tr>
        <tr>
            <td>Connally Memorial Medical Center</td>
            <td>Floresville</td>
            <td>TX</td>
            <td>3163.0</td>
        </tr>
        <tr>
            <td>Baylor Emergency Medical Center At Aubrey</td>
            <td>Aubrey</td>
            <td>TX</td>
            <td>3164.0</td>
        </tr>
        <tr>
            <td>Municipal Hospital and Granite Manor</td>
            <td>Granite Falls</td>
            <td>MN</td>
            <td>3165.0</td>
        </tr>
        <tr>
            <td>North Country Hospital</td>
            <td>Newport</td>
            <td>VT</td>
            <td>3166.0</td>
        </tr>
        <tr>
            <td>York General Hospital</td>
            <td>York</td>
            <td>NE</td>
            <td>3167.0</td>
        </tr>
        <tr>
            <td>Bellville St. Joseph Health Center</td>
            <td>Bellville</td>
            <td>TX</td>
            <td>3168.0</td>
        </tr>
        <tr>
            <td>Lakeland Community Hospital</td>
            <td>Haleyville</td>
            <td>AL</td>
            <td>3169.0</td>
        </tr>
        <tr>
            <td>Monument Health Custer Hospital</td>
            <td>Custer</td>
            <td>SD</td>
            <td>3170.0</td>
        </tr>
        <tr>
            <td>Richland Memorial Hospital</td>
            <td>Olney</td>
            <td>IL</td>
            <td>3171.0</td>
        </tr>
        <tr>
            <td>Alleghany County Memorial Hospital</td>
            <td>Sparta</td>
            <td>NC</td>
            <td>3173.0</td>
        </tr>
        <tr>
            <td>Southern Coos Hospital &amp; Health Center</td>
            <td>Bandon</td>
            <td>OR</td>
            <td>3174.0</td>
        </tr>
        <tr>
            <td>Centra Care Health Paynesville</td>
            <td>Paynesville</td>
            <td>MN</td>
            <td>3175.0</td>
        </tr>
        <tr>
            <td>MahaskaÂ¬â€  Health Partnership</td>
            <td>Oskaloosa</td>
            <td>IA</td>
            <td>3177.0</td>
        </tr>
        <tr>
            <td>Regional Health Sturgis Hospital</td>
            <td>Sturgis</td>
            <td>SD</td>
            <td>3178.0</td>
        </tr>
        <tr>
            <td>Benewah Community Hospital</td>
            <td>St. Maries</td>
            <td>ID</td>
            <td>3179.0</td>
        </tr>
        <tr>
            <td>Coffee Regional Medical Center</td>
            <td>Douglas</td>
            <td>GA</td>
            <td>3180.0</td>
        </tr>
        <tr>
            <td>Kern Valley Healthcare District</td>
            <td>Lake Isabella</td>
            <td>CA</td>
            <td>3181.0</td>
        </tr>
        <tr>
            <td>Wayne Medical Center</td>
            <td>Waynesboro</td>
            <td>TN</td>
            <td>3182.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital and Manor</td>
            <td>Bainbridge</td>
            <td>GA</td>
            <td>3183.0</td>
        </tr>
        <tr>
            <td>Jackson Hospital</td>
            <td>Marianna</td>
            <td>FL</td>
            <td>3184.0</td>
        </tr>
        <tr>
            <td>North Caddo Medical Center</td>
            <td>Vivian</td>
            <td>LA</td>
            <td>3185.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Aurora</td>
            <td>Aurora</td>
            <td>MO</td>
            <td>3186.0</td>
        </tr>
        <tr>
            <td>Mt Ascutney Hospital</td>
            <td>Windsor</td>
            <td>VT</td>
            <td>3187.0</td>
        </tr>
        <tr>
            <td>Gunnison Valley Hospital</td>
            <td>Gunnison</td>
            <td>UT</td>
            <td>3188.0</td>
        </tr>
        <tr>
            <td>Compass Memorial Healthcare</td>
            <td>Marengo</td>
            <td>IA</td>
            <td>3189.0</td>
        </tr>
        <tr>
            <td>Franklin Hospital</td>
            <td>Benton</td>
            <td>IL</td>
            <td>3190.0</td>
        </tr>
        <tr>
            <td>Little Falls Hospital</td>
            <td>Little Falls</td>
            <td>NY</td>
            <td>3191.0</td>
        </tr>
        <tr>
            <td>The Medical Center at Scottsville</td>
            <td>Scottsville</td>
            <td>KY</td>
            <td>3192.0</td>
        </tr>
        <tr>
            <td>Baptist Memorial Hospital - Calhoun</td>
            <td>Calhoun City</td>
            <td>MS</td>
            <td>3193.0</td>
        </tr>
        <tr>
            <td>Greeley County Health Services</td>
            <td>Tribune</td>
            <td>KS</td>
            <td>3194.0</td>
        </tr>
        <tr>
            <td>Lincoln Hospital</td>
            <td>Davenport</td>
            <td>WA</td>
            <td>3195.0</td>
        </tr>
        <tr>
            <td>Spanish Peaks Regional Health Center</td>
            <td>Walsenburg</td>
            <td>CO</td>
            <td>3196.0</td>
        </tr>
        <tr>
            <td>Clearwater Valley Hospital &amp; Clinics</td>
            <td>Orofino</td>
            <td>ID</td>
            <td>3197.0</td>
        </tr>
        <tr>
            <td>Salem Memorial District Hospital</td>
            <td>Salem</td>
            <td>MO</td>
            <td>3198.0</td>
        </tr>
        <tr>
            <td>Haskell Memorial Hospital</td>
            <td>Haskell</td>
            <td>TX</td>
            <td>3199.0</td>
        </tr>
        <tr>
            <td>Pleasant Valley Hospital</td>
            <td>Point Pleasant</td>
            <td>WV</td>
            <td>3200.0</td>
        </tr>
        <tr>
            <td>Coquille Valley Hospital District</td>
            <td>Coquille</td>
            <td>OR</td>
            <td>3201.0</td>
        </tr>
        <tr>
            <td>Sheridan Memorial Hosptial</td>
            <td>Plentywood</td>
            <td>MT</td>
            <td>3202.0</td>
        </tr>
        <tr>
            <td>Manning Regional Healthcare Center</td>
            <td>Manning</td>
            <td>IA</td>
            <td>3203.0</td>
        </tr>
        <tr>
            <td>Chase County Community Hospital</td>
            <td>Imperial</td>
            <td>NE</td>
            <td>3204.0</td>
        </tr>
        <tr>
            <td>Field Health System</td>
            <td>Centreville</td>
            <td>MS</td>
            <td>3205.0</td>
        </tr>
        <tr>
            <td>Regional Health Lead-Deadwood Hospital</td>
            <td>Deadwood</td>
            <td>SD</td>
            <td>3206.0</td>
        </tr>
        <tr>
            <td>Blue Mountain Hospital</td>
            <td>John Day</td>
            <td>OR</td>
            <td>3207.0</td>
        </tr>
        <tr>
            <td>Carlinville Area Hospital</td>
            <td>Carlinville</td>
            <td>IL</td>
            <td>3208.0</td>
        </tr>
        <tr>
            <td>Richardson Medical Center</td>
            <td>Rayville</td>
            <td>LA</td>
            <td>3209.0</td>
        </tr>
        <tr>
            <td>Henderson County Community Hospital</td>
            <td>Lexington</td>
            <td>TN</td>
            <td>3210.0</td>
        </tr>
        <tr>
            <td>Nocona General Hospital</td>
            <td>Nocona</td>
            <td>TX</td>
            <td>3211.0</td>
        </tr>
        <tr>
            <td>Mercy St. Francis Hospital</td>
            <td>Mountain View</td>
            <td>MO</td>
            <td>3212.0</td>
        </tr>
        <tr>
            <td>Memorial Community Hospital &amp; Health System</td>
            <td>Blair</td>
            <td>NE</td>
            <td>3213.0</td>
        </tr>
        <tr>
            <td>Stillwater Billings Clinic</td>
            <td>Columbus</td>
            <td>MT</td>
            <td>3214.0</td>
        </tr>
        <tr>
            <td>Kit Carson County Memorial Hospital</td>
            <td>Burlington</td>
            <td>CO</td>
            <td>3215.0</td>
        </tr>
        <tr>
            <td>Monroe Regional Hospital</td>
            <td>Aberdeen</td>
            <td>MS</td>
            <td>3216.0</td>
        </tr>
        <tr>
            <td>Mt. Edgecumbe Medical Center</td>
            <td>Sitka</td>
            <td>AK</td>
            <td>3217.0</td>
        </tr>
        <tr>
            <td>UnityPoint Health - Keokuk</td>
            <td>Keokuk</td>
            <td>IA</td>
            <td>3218.0</td>
        </tr>
        <tr>
            <td>Delta Memorial Hospital</td>
            <td>Dumas</td>
            <td>AR</td>
            <td>3219.0</td>
        </tr>
        <tr>
            <td>Newman Memorial Hospital</td>
            <td>Shattuck</td>
            <td>OK</td>
            <td>3220.0</td>
        </tr>
        <tr>
            <td>Palo Verde Hospital</td>
            <td>Blythe</td>
            <td>CA</td>
            <td>3221.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Waldron</td>
            <td>Waldron</td>
            <td>AR</td>
            <td>3222.0</td>
        </tr>
        <tr>
            <td>Clarinda Regional Health Center</td>
            <td>Clarinda</td>
            <td>IA</td>
            <td>3223.0</td>
        </tr>
        <tr>
            <td>Lincoln Health Hospital</td>
            <td>Hugo</td>
            <td>CO</td>
            <td>3224.0</td>
        </tr>
        <tr>
            <td>Pushmataha Hospital</td>
            <td>Antlers</td>
            <td>OK</td>
            <td>3225.0</td>
        </tr>
        <tr>
            <td>Ed Fraser Memorial Hospital</td>
            <td>Macclenny</td>
            <td>FL</td>
            <td>3226.0</td>
        </tr>
        <tr>
            <td>Baylor Scott And White Emergency Hospital</td>
            <td>Burleson</td>
            <td>TX</td>
            <td>3227.0</td>
        </tr>
        <tr>
            <td>Lavaca Medical Center</td>
            <td>Hallettsville</td>
            <td>TX</td>
            <td>3228.0</td>
        </tr>
        <tr>
            <td>Breckinridge Memorial Hospital</td>
            <td>Hardinsburg</td>
            <td>KY</td>
            <td>3229.0</td>
        </tr>
        <tr>
            <td>Marias Medical Center</td>
            <td>Shelby</td>
            <td>MT</td>
            <td>3230.0</td>
        </tr>
        <tr>
            <td>Sumner County Hospital District No 1</td>
            <td>Caldwell</td>
            <td>KS</td>
            <td>3231.0</td>
        </tr>
        <tr>
            <td>Lallie Kemp Medical Center</td>
            <td>Independence</td>
            <td>LA</td>
            <td>3232.0</td>
        </tr>
        <tr>
            <td>Barrett Hospital &amp; Healthcare</td>
            <td>Dillon</td>
            <td>MT</td>
            <td>3233.0</td>
        </tr>
        <tr>
            <td>The Medical Center at Albany</td>
            <td>Albany</td>
            <td>KY</td>
            <td>3234.0</td>
        </tr>
        <tr>
            <td>North Big Horn Hospital District</td>
            <td>Lovell</td>
            <td>WY</td>
            <td>3235.0</td>
        </tr>
        <tr>
            <td>Barnesville Hospital Association</td>
            <td>Barnesville</td>
            <td>OH</td>
            <td>3236.0</td>
        </tr>
        <tr>
            <td>Colorado River Medical Center</td>
            <td>Needles</td>
            <td>CA</td>
            <td>3237.0</td>
        </tr>
        <tr>
            <td>Sabine County Hospital</td>
            <td>Hemphill</td>
            <td>TX</td>
            <td>3238.0</td>
        </tr>
        <tr>
            <td>Three Rivers Hospital</td>
            <td>Brewster</td>
            <td>WA</td>
            <td>3239.0</td>
        </tr>
        <tr>
            <td>Schuyler Hospital</td>
            <td>Montour Falls</td>
            <td>NY</td>
            <td>3240.0</td>
        </tr>
        <tr>
            <td>Baptist Medical Center-Yazoo</td>
            <td>Yazoo City</td>
            <td>MS</td>
            <td>3241.0</td>
        </tr>
        <tr>
            <td>Lake District Hospital</td>
            <td>Lakeview</td>
            <td>OR</td>
            <td>3242.0</td>
        </tr>
        <tr>
            <td>Cook Hospital</td>
            <td>Cook</td>
            <td>MN</td>
            <td>3243.0</td>
        </tr>
        <tr>
            <td>Prowers Medical Center</td>
            <td>Lamar</td>
            <td>CO</td>
            <td>3244.0</td>
        </tr>
        <tr>
            <td>Endless Mountains Health Systems</td>
            <td>Montrose</td>
            <td>PA</td>
            <td>3245.0</td>
        </tr>
        <tr>
            <td>Laird Hospital</td>
            <td>Union</td>
            <td>MS</td>
            <td>3246.0</td>
        </tr>
        <tr>
            <td>Eureka Springs Hospital</td>
            <td>Eureka Springs</td>
            <td>AR</td>
            <td>3247.0</td>
        </tr>
        <tr>
            <td>Neosho Memorial Regional Medical Center</td>
            <td>Chanute</td>
            <td>KS</td>
            <td>3248.0</td>
        </tr>
        <tr>
            <td>Perham Health</td>
            <td>Perham</td>
            <td>MN</td>
            <td>3249.0</td>
        </tr>
        <tr>
            <td>J Arthur Dosher Memorial Hospital</td>
            <td>Southport</td>
            <td>NC</td>
            <td>3250.0</td>
        </tr>
        <tr>
            <td>Beaufort County Memorial Hospital</td>
            <td>Beaufort</td>
            <td>SC</td>
            <td>3251.0</td>
        </tr>
        <tr>
            <td>Crossroads Community Hospital</td>
            <td>Mount Vernon</td>
            <td>IL</td>
            <td>3252.0</td>
        </tr>
        <tr>
            <td>Thomas Hospital</td>
            <td>Fairhope</td>
            <td>AL</td>
            <td>3253.0</td>
        </tr>
        <tr>
            <td>The Outer Banks Hospital</td>
            <td>Nags Head</td>
            <td>NC</td>
            <td>3254.0</td>
        </tr>
        <tr>
            <td>Peterson Regional Medical Center</td>
            <td>Kerrville</td>
            <td>TX</td>
            <td>3255.0</td>
        </tr>
        <tr>
            <td>Memorial Regional Hospital</td>
            <td>Hollywood</td>
            <td>FL</td>
            <td>3256.0</td>
        </tr>
        <tr>
            <td>The Villages Regional Hospital</td>
            <td>The Villages</td>
            <td>FL</td>
            <td>3257.0</td>
        </tr>
        <tr>
            <td>Phelps Memorial Hospital Assn</td>
            <td>Sleepy Hollow</td>
            <td>NY</td>
            <td>3258.0</td>
        </tr>
        <tr>
            <td>Havasu Regional Medical Center</td>
            <td>Lake Havasu City</td>
            <td>AZ</td>
            <td>3259.0</td>
        </tr>
        <tr>
            <td>Pomerene Hospital</td>
            <td>Millersburg</td>
            <td>OH</td>
            <td>3260.0</td>
        </tr>
        <tr>
            <td>Palestine Regional Medical Center</td>
            <td>Palestine</td>
            <td>TX</td>
            <td>3261.0</td>
        </tr>
        <tr>
            <td>Clinch Valley Medical Center</td>
            <td>Richlands</td>
            <td>VA</td>
            <td>3262.0</td>
        </tr>
        <tr>
            <td>Bayhealth Hospital, Kent Campus</td>
            <td>Dover</td>
            <td>DE</td>
            <td>3263.0</td>
        </tr>
        <tr>
            <td>Vista Medical Center East</td>
            <td>Waukegan</td>
            <td>IL</td>
            <td>3264.0</td>
        </tr>
        <tr>
            <td>GHS Baptist Easley Hospital</td>
            <td>Easley</td>
            <td>SC</td>
            <td>3265.0</td>
        </tr>
        <tr>
            <td>Jackson Purchase Medical Center</td>
            <td>Mayfield</td>
            <td>KY</td>
            <td>3266.0</td>
        </tr>
        <tr>
            <td>Tanner Medical Center - Carrollton</td>
            <td>Carrollton</td>
            <td>GA</td>
            <td>3267.0</td>
        </tr>
        <tr>
            <td>Brandywine Hospital</td>
            <td>Coatesville</td>
            <td>PA</td>
            <td>3269.0</td>
        </tr>
        <tr>
            <td>AHMC Anaheim Regional Medical Center</td>
            <td>Anaheim</td>
            <td>CA</td>
            <td>3270.0</td>
        </tr>
        <tr>
            <td>Steward Rockledge Hospital</td>
            <td>Rockledge</td>
            <td>FL</td>
            <td>3271.0</td>
        </tr>
        <tr>
            <td>Christus St. Frances Cabrini Hospital</td>
            <td>Alexandria</td>
            <td>LA</td>
            <td>3272.0</td>
        </tr>
        <tr>
            <td>Centrastate Medical Center</td>
            <td>Freehold</td>
            <td>NJ</td>
            <td>3273.0</td>
        </tr>
        <tr>
            <td>Navicent Health Baldwin</td>
            <td>Milledgeville</td>
            <td>GA</td>
            <td>3274.0</td>
        </tr>
        <tr>
            <td>Lake Norman Regional Medical Center</td>
            <td>Mooresville</td>
            <td>NC</td>
            <td>3275.0</td>
        </tr>
        <tr>
            <td>Martin Medical Center</td>
            <td>Stuart</td>
            <td>FL</td>
            <td>3276.0</td>
        </tr>
        <tr>
            <td>Carlisle Regional Medical Center</td>
            <td>Carlisle</td>
            <td>PA</td>
            <td>3277.0</td>
        </tr>
        <tr>
            <td>Christus Health Shreveport - Bossier</td>
            <td>Shreveport</td>
            <td>LA</td>
            <td>3278.0</td>
        </tr>
        <tr>
            <td>Good Samaritan Medical Center</td>
            <td>West Palm Beach</td>
            <td>FL</td>
            <td>3279.0</td>
        </tr>
        <tr>
            <td>Merit Health Wesley</td>
            <td>Hattiesburg</td>
            <td>MS</td>
            <td>3280.0</td>
        </tr>
        <tr>
            <td>Sinai Hospital of Baltimore</td>
            <td>Baltimore</td>
            <td>MD</td>
            <td>3281.0</td>
        </tr>
        <tr>
            <td>Mcleod Regional Medical Center-Pee Dee</td>
            <td>Florence</td>
            <td>SC</td>
            <td>3282.0</td>
        </tr>
        <tr>
            <td>Betsy Johnson RegionalÂ¬â€  Hospital</td>
            <td>Dunn</td>
            <td>NC</td>
            <td>3283.0</td>
        </tr>
        <tr>
            <td>Navarro Regional Hospital</td>
            <td>Corsicana</td>
            <td>TX</td>
            <td>3284.0</td>
        </tr>
        <tr>
            <td>Highlands Regional Medical Center</td>
            <td>Sebring</td>
            <td>FL</td>
            <td>3285.0</td>
        </tr>
        <tr>
            <td>Magnolia Regional Health Center</td>
            <td>Corinth</td>
            <td>MS</td>
            <td>3286.0</td>
        </tr>
        <tr>
            <td>Oneida Health Hospital</td>
            <td>Oneida</td>
            <td>NY</td>
            <td>3287.0</td>
        </tr>
        <tr>
            <td>Southern Ocean Medical Center</td>
            <td>Manahawkin</td>
            <td>NJ</td>
            <td>3288.0</td>
        </tr>
        <tr>
            <td>Person Memorial Hospital</td>
            <td>Roxboro</td>
            <td>NC</td>
            <td>3289.0</td>
        </tr>
        <tr>
            <td>Thomas Memorial Hospital</td>
            <td>South Charleston</td>
            <td>WV</td>
            <td>3290.0</td>
        </tr>
        <tr>
            <td>McAlester Regional Health Center</td>
            <td>McAlester</td>
            <td>OK</td>
            <td>3291.0</td>
        </tr>
        <tr>
            <td>Sarah Bush Lincoln Health Center</td>
            <td>Mattoon</td>
            <td>IL</td>
            <td>3292.0</td>
        </tr>
        <tr>
            <td>Yuma Regional Medical Center</td>
            <td>Yuma</td>
            <td>AZ</td>
            <td>3293.0</td>
        </tr>
        <tr>
            <td>Heartland Regional Medical Center</td>
            <td>Marion</td>
            <td>IL</td>
            <td>3294.0</td>
        </tr>
        <tr>
            <td>Placentia Linda Hospital</td>
            <td>Placentia</td>
            <td>CA</td>
            <td>3296.0</td>
        </tr>
        <tr>
            <td>Baptist Hospital of Miami</td>
            <td>Miami</td>
            <td>FL</td>
            <td>3297.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital Miramar</td>
            <td>Miramar</td>
            <td>FL</td>
            <td>3298.0</td>
        </tr>
        <tr>
            <td>Sullivan County Community Hospital</td>
            <td>Sullivan</td>
            <td>IN</td>
            <td>3299.0</td>
        </tr>
        <tr>
            <td>Olean General Hospital</td>
            <td>Olean</td>
            <td>NY</td>
            <td>3300.0</td>
        </tr>
        <tr>
            <td>Crossing Rivers Health Medical Center</td>
            <td>Prairie Du Chien</td>
            <td>WI</td>
            <td>3301.0</td>
        </tr>
        <tr>
            <td>Burke Medical Center</td>
            <td>Waynesboro</td>
            <td>GA</td>
            <td>3302.0</td>
        </tr>
        <tr>
            <td>Fauquier Hospital</td>
            <td>Warrenton</td>
            <td>VA</td>
            <td>3303.0</td>
        </tr>
        <tr>
            <td>MUSC Health Lancaster Medical Center</td>
            <td>Lancaster</td>
            <td>SC</td>
            <td>3304.0</td>
        </tr>
        <tr>
            <td>Arkansas Methodist Medical Center</td>
            <td>Paragould</td>
            <td>AR</td>
            <td>3305.0</td>
        </tr>
        <tr>
            <td>Glenwood Regional Medical Center</td>
            <td>West Monroe</td>
            <td>LA</td>
            <td>3306.0</td>
        </tr>
        <tr>
            <td>Davis Medical Center</td>
            <td>Elkins</td>
            <td>WV</td>
            <td>3307.0</td>
        </tr>
        <tr>
            <td>Merit Health Natchez</td>
            <td>Natchez</td>
            <td>MS</td>
            <td>3308.0</td>
        </tr>
        <tr>
            <td>Geisinger Jersey Shore Hospital</td>
            <td>Jersey Shore</td>
            <td>PA</td>
            <td>3309.0</td>
        </tr>
        <tr>
            <td>North Mississippi Medical Center-Gilmore Amory</td>
            <td>Amory</td>
            <td>MS</td>
            <td>3310.0</td>
        </tr>
        <tr>
            <td>Centracare Health System - Sauk Centre</td>
            <td>Sauk Centre</td>
            <td>MN</td>
            <td>3311.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital of Texas County</td>
            <td>Guymon</td>
            <td>OK</td>
            <td>3312.0</td>
        </tr>
        <tr>
            <td>Shoals Hospital</td>
            <td>Muscle Shoals</td>
            <td>AL</td>
            <td>3313.0</td>
        </tr>
        <tr>
            <td>Santa Cruz Valley Regional Hospital</td>
            <td>Green Valley</td>
            <td>AZ</td>
            <td>3314.0</td>
        </tr>
        <tr>
            <td>Winneshiek Medical Center</td>
            <td>Decorah</td>
            <td>IA</td>
            <td>3315.0</td>
        </tr>
        <tr>
            <td>Doctors Hospital</td>
            <td>Coral Gables</td>
            <td>FL</td>
            <td>3316.0</td>
        </tr>
        <tr>
            <td>Pinckneyville Community Hospital</td>
            <td>Pinckneyville</td>
            <td>IL</td>
            <td>3317.0</td>
        </tr>
        <tr>
            <td>Fulton County Medical Center</td>
            <td>McConnellsburg</td>
            <td>PA</td>
            <td>3318.0</td>
        </tr>
        <tr>
            <td>Hills &amp; Dales General Hospital</td>
            <td>Cass City</td>
            <td>MI</td>
            <td>3319.0</td>
        </tr>
        <tr>
            <td>Texas County Memorial Hospital</td>
            <td>Houston</td>
            <td>MO</td>
            <td>3320.0</td>
        </tr>
        <tr>
            <td>Preston Memorial Hospital</td>
            <td>Kingwood</td>
            <td>WV</td>
            <td>3321.0</td>
        </tr>
        <tr>
            <td>D.W. McMillan Memorial Hospital</td>
            <td>Brewton</td>
            <td>AL</td>
            <td>3322.0</td>
        </tr>
        <tr>
            <td>Kentucky River Medical Center</td>
            <td>Jackson</td>
            <td>KY</td>
            <td>3323.0</td>
        </tr>
        <tr>
            <td>Stevens Community Medical Center</td>
            <td>Morris</td>
            <td>MN</td>
            <td>3324.0</td>
        </tr>
        <tr>
            <td>Westchester General Hospital</td>
            <td>Miami</td>
            <td>FL</td>
            <td>3325.0</td>
        </tr>
        <tr>
            <td>Ohio County Hospital</td>
            <td>Hartford</td>
            <td>KY</td>
            <td>3326.0</td>
        </tr>
        <tr>
            <td>Garfield Memorial Hospital</td>
            <td>Panguitch</td>
            <td>UT</td>
            <td>3327.0</td>
        </tr>
        <tr>
            <td>Morton County Hospital</td>
            <td>Elkhart</td>
            <td>KS</td>
            <td>3328.0</td>
        </tr>
        <tr>
            <td>Sabetha Community Hospital</td>
            <td>Sabetha</td>
            <td>KS</td>
            <td>3329.0</td>
        </tr>
        <tr>
            <td>Pike County Memorial Hospital</td>
            <td>Louisiana</td>
            <td>MO</td>
            <td>3330.0</td>
        </tr>
        <tr>
            <td>Morrow County Hospital</td>
            <td>Mount Gilead</td>
            <td>OH</td>
            <td>3331.0</td>
        </tr>
        <tr>
            <td>Mizell Memorial Hospital</td>
            <td>Opp</td>
            <td>AL</td>
            <td>3332.0</td>
        </tr>
        <tr>
            <td>Mitchell County Regional Health</td>
            <td>Osage</td>
            <td>IA</td>
            <td>3333.0</td>
        </tr>
        <tr>
            <td>Livingston Hospital And Healthcare Services</td>
            <td>Salem</td>
            <td>KY</td>
            <td>3334.0</td>
        </tr>
        <tr>
            <td>Monroe County Hospital</td>
            <td>Monroeville</td>
            <td>AL</td>
            <td>3335.0</td>
        </tr>
        <tr>
            <td>Sheridan County Hospital</td>
            <td>Hoxie</td>
            <td>KS</td>
            <td>3336.0</td>
        </tr>
        <tr>
            <td>Larkin Community Hospital Palm Springs Campus</td>
            <td>Hialeah</td>
            <td>FL</td>
            <td>3337.0</td>
        </tr>
        <tr>
            <td>Red Bay Hospital</td>
            <td>Red Bay</td>
            <td>AL</td>
            <td>3338.0</td>
        </tr>
        <tr>
            <td>Madison Hospital</td>
            <td>Madison</td>
            <td>MN</td>
            <td>3339.0</td>
        </tr>
        <tr>
            <td>Washington County Regional Medical Center</td>
            <td>Sandersville</td>
            <td>GA</td>
            <td>3340.0</td>
        </tr>
        <tr>
            <td>Wayne Memorial Hospital</td>
            <td>Jesup</td>
            <td>GA</td>
            <td>3341.0</td>
        </tr>
        <tr>
            <td>Iowa Specialty Hospital - Belmond</td>
            <td>Belmond</td>
            <td>IA</td>
            <td>3342.0</td>
        </tr>
        <tr>
            <td>Webster General Hospital/ Swing Bed</td>
            <td>Eupora</td>
            <td>MS</td>
            <td>3343.0</td>
        </tr>
        <tr>
            <td>LECOM Health Corry Memorial Hospital</td>
            <td>Corry</td>
            <td>PA</td>
            <td>3344.0</td>
        </tr>
        <tr>
            <td>Thayer County Health Services</td>
            <td>Hebron</td>
            <td>NE</td>
            <td>3345.0</td>
        </tr>
        <tr>
            <td>Stonewall Memorial Hospital</td>
            <td>Aspermont</td>
            <td>TX</td>
            <td>3346.0</td>
        </tr>
        <tr>
            <td>Kalkaska Memorial Health Center</td>
            <td>Kalkaska</td>
            <td>MI</td>
            <td>3348.0</td>
        </tr>
        <tr>
            <td>Elmore Community Hospital</td>
            <td>Wetumpka</td>
            <td>AL</td>
            <td>3349.0</td>
        </tr>
        <tr>
            <td>Allen County Regional Hospital</td>
            <td>Iola</td>
            <td>KS</td>
            <td>3350.0</td>
        </tr>
        <tr>
            <td>Rockcastle Regional Hospital &amp; Respiratory Care Ct</td>
            <td>Mount Vernon</td>
            <td>KY</td>
            <td>3351.0</td>
        </tr>
        <tr>
            <td>Ray County Memorial Hospital</td>
            <td>Richmond</td>
            <td>MO</td>
            <td>3352.0</td>
        </tr>
        <tr>
            <td>Perry County Memorial Hospital</td>
            <td>Tell City</td>
            <td>IN</td>
            <td>3353.0</td>
        </tr>
        <tr>
            <td>Madison County Memorial Hospital</td>
            <td>Madison</td>
            <td>FL</td>
            <td>3354.0</td>
        </tr>
        <tr>
            <td>Barbourville ARH Hospital</td>
            <td>Barbourville</td>
            <td>KY</td>
            <td>3355.0</td>
        </tr>
        <tr>
            <td>Larkin Community Hospital</td>
            <td>South Miami</td>
            <td>FL</td>
            <td>3356.0</td>
        </tr>
        <tr>
            <td>Mason District Hospital</td>
            <td>Havana</td>
            <td>IL</td>
            <td>3358.0</td>
        </tr>
        <tr>
            <td>Murray County Memorial Hospital</td>
            <td>Slayton</td>
            <td>MN</td>
            <td>3359.0</td>
        </tr>
        <tr>
            <td>Chicot Memorial Medical Center</td>
            <td>Lake Village</td>
            <td>AR</td>
            <td>3360.0</td>
        </tr>
        <tr>
            <td>Regional Health Services Of Howard County</td>
            <td>Cresco</td>
            <td>IA</td>
            <td>3361.0</td>
        </tr>
        <tr>
            <td>Piggott Community Hospital</td>
            <td>Piggott</td>
            <td>AR</td>
            <td>3362.0</td>
        </tr>
        <tr>
            <td>Lake Chelan Community Hospital</td>
            <td>Chelan</td>
            <td>WA</td>
            <td>3363.0</td>
        </tr>
        <tr>
            <td>Greene County General Hospital</td>
            <td>Linton</td>
            <td>IN</td>
            <td>3364.0</td>
        </tr>
        <tr>
            <td>Holton Community Hospital</td>
            <td>Holton</td>
            <td>KS</td>
            <td>3365.0</td>
        </tr>
        <tr>
            <td>Henry County Health Center</td>
            <td>Mount Pleasant</td>
            <td>IA</td>
            <td>3366.0</td>
        </tr>
        <tr>
            <td>Beartooth Billings Clinic</td>
            <td>Red Lodge</td>
            <td>MT</td>
            <td>3367.0</td>
        </tr>
        <tr>
            <td>Gordon Memorial Hospital District</td>
            <td>Gordon</td>
            <td>NE</td>
            <td>3368.0</td>
        </tr>
        <tr>
            <td>Baptist Medical Center Attala</td>
            <td>Kosciusko</td>
            <td>MS</td>
            <td>3369.0</td>
        </tr>
        <tr>
            <td>Ellsworth County Medical Center</td>
            <td>Ellsworth</td>
            <td>KS</td>
            <td>3370.0</td>
        </tr>
        <tr>
            <td>Dorminy Medical Center</td>
            <td>Fitzgerald</td>
            <td>GA</td>
            <td>3371.0</td>
        </tr>
        <tr>
            <td>Cass County Memorial Hospital</td>
            <td>Atlantic</td>
            <td>IA</td>
            <td>3372.0</td>
        </tr>
        <tr>
            <td>Goodland Regional Medical Center</td>
            <td>Goodland</td>
            <td>KS</td>
            <td>3373.0</td>
        </tr>
        <tr>
            <td>Scott County Hospital</td>
            <td>Scott City</td>
            <td>KS</td>
            <td>3374.0</td>
        </tr>
        <tr>
            <td>Hillcrest Hospital Henryetta</td>
            <td>Henryetta</td>
            <td>OK</td>
            <td>3375.0</td>
        </tr>
        <tr>
            <td>Spectrum Health Reed City Hospital</td>
            <td>Reed City</td>
            <td>MI</td>
            <td>3376.0</td>
        </tr>
        <tr>
            <td>Virginia Gay Hospital</td>
            <td>Vinton</td>
            <td>IA</td>
            <td>3379.0</td>
        </tr>
        <tr>
            <td>Pershing Memorial Hospital</td>
            <td>Brookfield</td>
            <td>MO</td>
            <td>3380.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital of Lafayette County</td>
            <td>Darlington</td>
            <td>WI</td>
            <td>3381.0</td>
        </tr>
        <tr>
            <td>Osborne County Memorial Hospital</td>
            <td>Osborne</td>
            <td>KS</td>
            <td>3382.0</td>
        </tr>
        <tr>
            <td>Aspirus Ontonagon Hospital</td>
            <td>Ontonagon</td>
            <td>MI</td>
            <td>3383.0</td>
        </tr>
        <tr>
            <td>North Sunflower Medical Center Cah</td>
            <td>Ruleville</td>
            <td>MS</td>
            <td>3384.0</td>
        </tr>
        <tr>
            <td>Avera Dells Area Hospital  - CAH</td>
            <td>Dell Rapids</td>
            <td>SD</td>
            <td>3385.0</td>
        </tr>
        <tr>
            <td>Wilson Medical Center</td>
            <td>Neodesha</td>
            <td>KS</td>
            <td>3386.0</td>
        </tr>
        <tr>
            <td>Northwest Florida Community Hospital</td>
            <td>Chipley</td>
            <td>FL</td>
            <td>3387.0</td>
        </tr>
        <tr>
            <td>Edwards County Hospital</td>
            <td>Kinsley</td>
            <td>KS</td>
            <td>3388.0</td>
        </tr>
        <tr>
            <td>Kingman Community Hospital</td>
            <td>Kingman</td>
            <td>KS</td>
            <td>3389.0</td>
        </tr>
        <tr>
            <td>Trego County Lemke Memorial Hospital</td>
            <td>WaKeeney</td>
            <td>KS</td>
            <td>3390.0</td>
        </tr>
        <tr>
            <td>West Carroll Memorial Hospital</td>
            <td>Oak Grove</td>
            <td>LA</td>
            <td>3391.0</td>
        </tr>
        <tr>
            <td>Soldiers and Sailors Memorial Hospital of Yates</td>
            <td>Penn Yan</td>
            <td>NY</td>
            <td>3392.0</td>
        </tr>
        <tr>
            <td>Monroe County Medical Center</td>
            <td>Tompkinsville</td>
            <td>KY</td>
            <td>3393.0</td>
        </tr>
        <tr>
            <td>Renville County Hospital and Clinics</td>
            <td>Olivia</td>
            <td>MN</td>
            <td>3394.0</td>
        </tr>
        <tr>
            <td>Bullock County Hospital</td>
            <td>Union Springs</td>
            <td>AL</td>
            <td>3395.0</td>
        </tr>
        <tr>
            <td>Methodist Hospital Union County</td>
            <td>Morganfield</td>
            <td>KY</td>
            <td>3396.0</td>
        </tr>
        <tr>
            <td>Horn Memorial Hospital</td>
            <td>Ida Grove</td>
            <td>IA</td>
            <td>3397.0</td>
        </tr>
        <tr>
            <td>Mangum Regional Medical Center</td>
            <td>Mangum</td>
            <td>OK</td>
            <td>3398.0</td>
        </tr>
        <tr>
            <td>Deer Lodge Medical Center - CAH</td>
            <td>Deer Lodge</td>
            <td>MT</td>
            <td>3399.0</td>
        </tr>
        <tr>
            <td>Winn Parish Medical Center</td>
            <td>Winnfield</td>
            <td>LA</td>
            <td>3400.0</td>
        </tr>
        <tr>
            <td>The James B Haggin Memorial Hospital</td>
            <td>Harrodsburg</td>
            <td>KY</td>
            <td>3401.0</td>
        </tr>
        <tr>
            <td>St. Luke Hospital &amp; Living Center</td>
            <td>Marion</td>
            <td>KS</td>
            <td>3402.0</td>
        </tr>
        <tr>
            <td>St. Joseph&#x27;s Medical Center</td>
            <td>Yonkers</td>
            <td>NY</td>
            <td>3403.0</td>
        </tr>
        <tr>
            <td>St. John&#x27;s Episcopal Hospital at South Shore</td>
            <td>Far Rockaway</td>
            <td>NY</td>
            <td>3404.0</td>
        </tr>
        <tr>
            <td>Jennie Stuart Medical Center</td>
            <td>Hopkinsville</td>
            <td>KY</td>
            <td>3405.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital of Converse County</td>
            <td>Douglas</td>
            <td>WY</td>
            <td>3406.0</td>
        </tr>
        <tr>
            <td>Huron Regional Medical Center</td>
            <td>Huron</td>
            <td>SD</td>
            <td>3407.0</td>
        </tr>
        <tr>
            <td>Hot Springs County Memorial Hospital</td>
            <td>Thermopolis</td>
            <td>WY</td>
            <td>3408.0</td>
        </tr>
        <tr>
            <td>Fulton County Hospital</td>
            <td>Salem</td>
            <td>AR</td>
            <td>3409.0</td>
        </tr>
        <tr>
            <td>St. Francis Memorial Hospital</td>
            <td>West Point</td>
            <td>NE</td>
            <td>3410.0</td>
        </tr>
        <tr>
            <td>Copper Queen Community Hospital</td>
            <td>Bisbee</td>
            <td>AZ</td>
            <td>3411.0</td>
        </tr>
        <tr>
            <td>Cherokee Regional Medical Center</td>
            <td>Cherokee</td>
            <td>IA</td>
            <td>3412.0</td>
        </tr>
        <tr>
            <td>Madison Regional Health System</td>
            <td>Madison</td>
            <td>SD</td>
            <td>3414.0</td>
        </tr>
        <tr>
            <td>Burgess Health Center</td>
            <td>Onawa</td>
            <td>IA</td>
            <td>3415.0</td>
        </tr>
        <tr>
            <td>Cameron Regional Medical Center</td>
            <td>Cameron</td>
            <td>MO</td>
            <td>3416.0</td>
        </tr>
        <tr>
            <td>Wayne General Hospital</td>
            <td>Waynesboro</td>
            <td>MS</td>
            <td>3417.0</td>
        </tr>
        <tr>
            <td>Panola Medical Center</td>
            <td>Batesville</td>
            <td>MS</td>
            <td>3418.0</td>
        </tr>
        <tr>
            <td>Clarion Hospital</td>
            <td>Clarion</td>
            <td>PA</td>
            <td>3419.0</td>
        </tr>
        <tr>
            <td>Morehouse General Hospital</td>
            <td>Bastrop</td>
            <td>LA</td>
            <td>3420.0</td>
        </tr>
        <tr>
            <td>Russell County Hospital</td>
            <td>Russell Springs</td>
            <td>KY</td>
            <td>3421.0</td>
        </tr>
        <tr>
            <td>Syringa General Hospital</td>
            <td>Grangeville</td>
            <td>ID</td>
            <td>3422.0</td>
        </tr>
        <tr>
            <td>Community Hospital Association</td>
            <td>Fairfax</td>
            <td>MO</td>
            <td>3423.0</td>
        </tr>
        <tr>
            <td>Clay County Medical Center</td>
            <td>Clay Center</td>
            <td>KS</td>
            <td>3424.0</td>
        </tr>
        <tr>
            <td>Upson Regional Medical Center</td>
            <td>Thomaston</td>
            <td>GA</td>
            <td>3425.0</td>
        </tr>
        <tr>
            <td>Choctaw Memorial Hospital</td>
            <td>Hugo</td>
            <td>OK</td>
            <td>3426.0</td>
        </tr>
        <tr>
            <td>Lucas County Health Center</td>
            <td>Chariton</td>
            <td>IA</td>
            <td>3427.0</td>
        </tr>
        <tr>
            <td>Reeves County Hospital District</td>
            <td>Pecos</td>
            <td>TX</td>
            <td>3428.0</td>
        </tr>
        <tr>
            <td>Cloud County Health Center</td>
            <td>Concordia</td>
            <td>KS</td>
            <td>3429.0</td>
        </tr>
        <tr>
            <td>Hardin County General Hospital</td>
            <td>Rosiclare</td>
            <td>IL</td>
            <td>3430.0</td>
        </tr>
        <tr>
            <td>Jane Todd Crawford Hospital</td>
            <td>Greensburg</td>
            <td>KY</td>
            <td>3431.0</td>
        </tr>
        <tr>
            <td>Jacobson Memorial Hospital Care Center</td>
            <td>Elgin</td>
            <td>ND</td>
            <td>3432.0</td>
        </tr>
        <tr>
            <td>Pemiscot County Memorial Hospital</td>
            <td>Hayti</td>
            <td>MO</td>
            <td>3433.0</td>
        </tr>
        <tr>
            <td>Ridgeview Sibley Medical Center</td>
            <td>Arlington</td>
            <td>MN</td>
            <td>3435.0</td>
        </tr>
        <tr>
            <td>The Medical Center at Caverna</td>
            <td>Horse Cave</td>
            <td>KY</td>
            <td>3436.0</td>
        </tr>
        <tr>
            <td>Graham County Hospital</td>
            <td>Hill City</td>
            <td>KS</td>
            <td>3437.0</td>
        </tr>
        <tr>
            <td>Holmes County Hospital and Clinics</td>
            <td>Lexington</td>
            <td>MS</td>
            <td>3438.0</td>
        </tr>
        <tr>
            <td>Guadalupe County Hospital</td>
            <td>Santa Rosa</td>
            <td>NM</td>
            <td>3439.0</td>
        </tr>
        <tr>
            <td>Riverland Medical Center</td>
            <td>Ferriday</td>
            <td>LA</td>
            <td>3440.0</td>
        </tr>
        <tr>
            <td>Clara Barton Hospital</td>
            <td>Hoisington</td>
            <td>KS</td>
            <td>3441.0</td>
        </tr>
        <tr>
            <td>Coleman County Medical Center Company</td>
            <td>Coleman</td>
            <td>TX</td>
            <td>3442.0</td>
        </tr>
        <tr>
            <td>Mobridge Regional Hospital</td>
            <td>Mobridge</td>
            <td>SD</td>
            <td>3443.0</td>
        </tr>
        <tr>
            <td>Margaretville Memorial Hospital</td>
            <td>Margaretville</td>
            <td>NY</td>
            <td>3444.0</td>
        </tr>
        <tr>
            <td>Adams County Regional Medical Center</td>
            <td>Seaman</td>
            <td>OH</td>
            <td>3445.0</td>
        </tr>
        <tr>
            <td>Elizabethtown Community Hospital</td>
            <td>Elizabethtown</td>
            <td>NY</td>
            <td>3446.0</td>
        </tr>
        <tr>
            <td>Union County General Hospital</td>
            <td>Clayton</td>
            <td>NM</td>
            <td>3447.0</td>
        </tr>
        <tr>
            <td>Mid Valley Hospital</td>
            <td>Omak</td>
            <td>WA</td>
            <td>3449.0</td>
        </tr>
        <tr>
            <td>Hanover Hospital</td>
            <td>Hanover</td>
            <td>KS</td>
            <td>3450.0</td>
        </tr>
        <tr>
            <td>Trinity Hospital</td>
            <td>Wolf Point</td>
            <td>MT</td>
            <td>3451.0</td>
        </tr>
        <tr>
            <td>AllianceHealth Madill</td>
            <td>Madill</td>
            <td>OK</td>
            <td>3452.0</td>
        </tr>
        <tr>
            <td>Ascension St. John Nowata</td>
            <td>Nowata</td>
            <td>OK</td>
            <td>3453.0</td>
        </tr>
        <tr>
            <td>River Valley Medical Center</td>
            <td>Dardanelle</td>
            <td>AR</td>
            <td>3454.0</td>
        </tr>
        <tr>
            <td>Scott Regional Hospital Cah</td>
            <td>Morton</td>
            <td>MS</td>
            <td>3455.0</td>
        </tr>
        <tr>
            <td>Creek Nation Community Hospital</td>
            <td>Okemah</td>
            <td>OK</td>
            <td>3456.0</td>
        </tr>
        <tr>
            <td>John C Stennis Memorial Hospital</td>
            <td>De Kalb</td>
            <td>MS</td>
            <td>3457.0</td>
        </tr>
        <tr>
            <td>Trigg County Hospital</td>
            <td>Cadiz</td>
            <td>KY</td>
            <td>3458.0</td>
        </tr>
        <tr>
            <td>Palm Beach Gardens Medical Center</td>
            <td>Palm Beach Gardens</td>
            <td>FL</td>
            <td>3459.0</td>
        </tr>
        <tr>
            <td>Kansas Medical Center Llc</td>
            <td>Andover</td>
            <td>KS</td>
            <td>3460.0</td>
        </tr>
        <tr>
            <td>South Miami Hospital</td>
            <td>South Miami</td>
            <td>FL</td>
            <td>3461.0</td>
        </tr>
        <tr>
            <td>Wiregrass Medical Center</td>
            <td>Geneva</td>
            <td>AL</td>
            <td>3462.0</td>
        </tr>
        <tr>
            <td>Effingham Health System</td>
            <td>Springfield</td>
            <td>GA</td>
            <td>3463.0</td>
        </tr>
        <tr>
            <td>Gove County Medical Center</td>
            <td>Quinter</td>
            <td>KS</td>
            <td>3464.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System Franciscan Healthcare Sparta</td>
            <td>Sparta</td>
            <td>WI</td>
            <td>3466.0</td>
        </tr>
        <tr>
            <td>Fairfield Memorial Hospital</td>
            <td>Fairfield</td>
            <td>IL</td>
            <td>3467.0</td>
        </tr>
        <tr>
            <td>Troy Regional Medical Center</td>
            <td>Troy</td>
            <td>AL</td>
            <td>3468.0</td>
        </tr>
        <tr>
            <td>Bradley County Medical Center</td>
            <td>Warren</td>
            <td>AR</td>
            <td>3469.0</td>
        </tr>
        <tr>
            <td>Appling Hospital</td>
            <td>Baxley</td>
            <td>GA</td>
            <td>3470.0</td>
        </tr>
        <tr>
            <td>Byrd Regional Hospital</td>
            <td>Leesville</td>
            <td>LA</td>
            <td>3471.0</td>
        </tr>
        <tr>
            <td>Cimarron Memorial Hospital</td>
            <td>Boise City</td>
            <td>OK</td>
            <td>3472.0</td>
        </tr>
        <tr>
            <td>Sparta Community Hospital</td>
            <td>Sparta</td>
            <td>IL</td>
            <td>3473.0</td>
        </tr>
        <tr>
            <td>Neshoba County General Hospital</td>
            <td>Philadelphia</td>
            <td>MS</td>
            <td>3474.0</td>
        </tr>
        <tr>
            <td>Bibb Medical Center</td>
            <td>Centreville</td>
            <td>AL</td>
            <td>3476.0</td>
        </tr>
        <tr>
            <td>Hodgeman County Health Center</td>
            <td>Jetmore</td>
            <td>KS</td>
            <td>3477.0</td>
        </tr>
        <tr>
            <td>Cobleskill Regional Hospital</td>
            <td>Cobleskill</td>
            <td>NY</td>
            <td>3479.0</td>
        </tr>
        <tr>
            <td>Phillips County Health Systems</td>
            <td>Phillipsburg</td>
            <td>KS</td>
            <td>3480.0</td>
        </tr>
        <tr>
            <td>Thomas H Boyd Memorial Hospital</td>
            <td>Carrollton</td>
            <td>IL</td>
            <td>3481.0</td>
        </tr>
        <tr>
            <td>Oakdale Community Hospital</td>
            <td>Oakdale</td>
            <td>LA</td>
            <td>3482.0</td>
        </tr>
        <tr>
            <td>Guthrie County Hospital</td>
            <td>Guthrie Center</td>
            <td>IA</td>
            <td>3483.0</td>
        </tr>
        <tr>
            <td>Frances Mahon Deaconess Hospital</td>
            <td>Glasgow</td>
            <td>MT</td>
            <td>3484.0</td>
        </tr>
        <tr>
            <td>Barnes-Kasson County Hospital</td>
            <td>Susquehanna</td>
            <td>PA</td>
            <td>3485.0</td>
        </tr>
        <tr>
            <td>Girard Medical Center</td>
            <td>Girard</td>
            <td>KS</td>
            <td>3486.0</td>
        </tr>
        <tr>
            <td>Jefferson Community Health &amp; Life</td>
            <td>Fairbury</td>
            <td>NE</td>
            <td>3487.0</td>
        </tr>
        <tr>
            <td>Caribou Memorial Hospital</td>
            <td>Soda Springs</td>
            <td>ID</td>
            <td>3488.0</td>
        </tr>
        <tr>
            <td>Avera Flandreau Hospital - CAH</td>
            <td>Flandreau</td>
            <td>SD</td>
            <td>3489.0</td>
        </tr>
        <tr>
            <td>Chadron Community Hospital Corp</td>
            <td>Chadron</td>
            <td>NE</td>
            <td>3490.0</td>
        </tr>
        <tr>
            <td>Smith County Memorial Hospital</td>
            <td>Smith Center</td>
            <td>KS</td>
            <td>3491.0</td>
        </tr>
        <tr>
            <td>Midwest Medical Center</td>
            <td>Galena</td>
            <td>IL</td>
            <td>3492.0</td>
        </tr>
        <tr>
            <td>Stevens County Hospital</td>
            <td>Hugoton</td>
            <td>KS</td>
            <td>3493.0</td>
        </tr>
        <tr>
            <td>Sabine Medical Center</td>
            <td>Many</td>
            <td>LA</td>
            <td>3494.0</td>
        </tr>
        <tr>
            <td>Bertrand Chaffee Hospital</td>
            <td>Springville</td>
            <td>NY</td>
            <td>3495.0</td>
        </tr>
        <tr>
            <td>Cozad Community Hospital</td>
            <td>Cozad</td>
            <td>NE</td>
            <td>3496.0</td>
        </tr>
        <tr>
            <td>Choctaw Regional Medical Center</td>
            <td>Ackerman</td>
            <td>MS</td>
            <td>3497.0</td>
        </tr>
        <tr>
            <td>Montgomery General Hospital</td>
            <td>Montgomery</td>
            <td>WV</td>
            <td>3498.0</td>
        </tr>
        <tr>
            <td>Cherry County Hospital</td>
            <td>Valentine</td>
            <td>NE</td>
            <td>3500.0</td>
        </tr>
        <tr>
            <td>Mitchell County Hospital Health Systems</td>
            <td>Beloit</td>
            <td>KS</td>
            <td>3501.0</td>
        </tr>
        <tr>
            <td>Ortonville Area Health Services</td>
            <td>Ortonville</td>
            <td>MN</td>
            <td>3502.0</td>
        </tr>
        <tr>
            <td>AdventHealth Durand</td>
            <td>Durand</td>
            <td>WI</td>
            <td>3504.0</td>
        </tr>
        <tr>
            <td>Herington Municipal Hospital</td>
            <td>Herington</td>
            <td>KS</td>
            <td>3505.0</td>
        </tr>
        <tr>
            <td>Valley County Health System</td>
            <td>Ord</td>
            <td>NE</td>
            <td>3506.0</td>
        </tr>
        <tr>
            <td>Audubon County Memorial Hospital</td>
            <td>Audubon</td>
            <td>IA</td>
            <td>3507.0</td>
        </tr>
        <tr>
            <td>Ellett Memorial Hospital</td>
            <td>Appleton City</td>
            <td>MO</td>
            <td>3508.0</td>
        </tr>
        <tr>
            <td>Mountain Lakes Medical Center</td>
            <td>Clayton</td>
            <td>GA</td>
            <td>3509.0</td>
        </tr>
        <tr>
            <td>Macon County Samaritan Memorial Hospital</td>
            <td>Macon</td>
            <td>MO</td>
            <td>3510.0</td>
        </tr>
        <tr>
            <td>Yuma District Hospital</td>
            <td>Yuma</td>
            <td>CO</td>
            <td>3511.0</td>
        </tr>
        <tr>
            <td>Ochiltree General Hospital</td>
            <td>Perryton</td>
            <td>TX</td>
            <td>3512.0</td>
        </tr>
        <tr>
            <td>Harrison County Community Hospital</td>
            <td>Bethany</td>
            <td>MO</td>
            <td>3513.0</td>
        </tr>
        <tr>
            <td>Hardtner Medical Center</td>
            <td>Olla</td>
            <td>LA</td>
            <td>3514.0</td>
        </tr>
        <tr>
            <td>Evergreen Medical Center</td>
            <td>Evergreen</td>
            <td>AL</td>
            <td>3515.0</td>
        </tr>
        <tr>
            <td>Washington County Memorial Hospital</td>
            <td>Potosi</td>
            <td>MO</td>
            <td>3516.0</td>
        </tr>
        <tr>
            <td>Avoyelles Hospital</td>
            <td>Marksville</td>
            <td>LA</td>
            <td>3517.0</td>
        </tr>
        <tr>
            <td>Russell Regional Hospital</td>
            <td>Russell</td>
            <td>KS</td>
            <td>3518.0</td>
        </tr>
        <tr>
            <td>Lasalle General Hospital</td>
            <td>Jena</td>
            <td>LA</td>
            <td>3519.0</td>
        </tr>
        <tr>
            <td>Antelope Memorial Hospital</td>
            <td>Neligh</td>
            <td>NE</td>
            <td>3520.0</td>
        </tr>
        <tr>
            <td>Miller County Hospital</td>
            <td>Colquitt</td>
            <td>GA</td>
            <td>3521.0</td>
        </tr>
        <tr>
            <td>Palo Alto County Hospital</td>
            <td>Emmetsburg</td>
            <td>IA</td>
            <td>3522.0</td>
        </tr>
        <tr>
            <td>North Valley Health Center</td>
            <td>Warren</td>
            <td>MN</td>
            <td>3523.0</td>
        </tr>
        <tr>
            <td>Ferrell Hospital Community Foundations</td>
            <td>Eldorado</td>
            <td>IL</td>
            <td>3524.0</td>
        </tr>
        <tr>
            <td>Tioga Medical Center</td>
            <td>Tioga</td>
            <td>ND</td>
            <td>3525.0</td>
        </tr>
        <tr>
            <td>Dewitt Hospital &amp; Nursing Home</td>
            <td>De Witt</td>
            <td>AR</td>
            <td>3527.0</td>
        </tr>
        <tr>
            <td>Fairview Regional Medical Center Authority</td>
            <td>Fairview</td>
            <td>OK</td>
            <td>3528.0</td>
        </tr>
        <tr>
            <td>Tri Valley Health System</td>
            <td>Cambridge</td>
            <td>NE</td>
            <td>3529.0</td>
        </tr>
        <tr>
            <td>Winston Medical Center &amp; Swingbed</td>
            <td>Louisville</td>
            <td>MS</td>
            <td>3530.0</td>
        </tr>
        <tr>
            <td>Benson Hospital</td>
            <td>Benson</td>
            <td>AZ</td>
            <td>3531.0</td>
        </tr>
        <tr>
            <td>Casey County Hospital</td>
            <td>Liberty</td>
            <td>KY</td>
            <td>3532.0</td>
        </tr>
        <tr>
            <td>Eastern Plumas Hospital - Portola Campus</td>
            <td>Portola</td>
            <td>CA</td>
            <td>3533.0</td>
        </tr>
        <tr>
            <td>Harmon Memorial Hospital</td>
            <td>Hollis</td>
            <td>OK</td>
            <td>3534.0</td>
        </tr>
        <tr>
            <td>Pana Community Hospital</td>
            <td>Pana</td>
            <td>IL</td>
            <td>3535.0</td>
        </tr>
        <tr>
            <td>Fayette County Hospital</td>
            <td>Vandalia</td>
            <td>IL</td>
            <td>3536.0</td>
        </tr>
        <tr>
            <td>Hans P Peterson Memorial Hospital - CAH</td>
            <td>Philip</td>
            <td>SD</td>
            <td>3537.0</td>
        </tr>
        <tr>
            <td>Mercy Medical Center-New Hampton</td>
            <td>New Hampton</td>
            <td>IA</td>
            <td>3538.0</td>
        </tr>
        <tr>
            <td>Hillsboro Area Hospital</td>
            <td>Hillsboro</td>
            <td>IL</td>
            <td>3539.0</td>
        </tr>
        <tr>
            <td>Buchanan County Health Center</td>
            <td>Independence</td>
            <td>IA</td>
            <td>3540.0</td>
        </tr>
        <tr>
            <td>Jackson County Regional Health Center</td>
            <td>Maquoketa</td>
            <td>IA</td>
            <td>3541.0</td>
        </tr>
        <tr>
            <td>Drumright Regional Hospital</td>
            <td>Drumright</td>
            <td>OK</td>
            <td>3542.0</td>
        </tr>
        <tr>
            <td>Hardeman County Memorial Hospital</td>
            <td>Quanah</td>
            <td>TX</td>
            <td>3543.0</td>
        </tr>
        <tr>
            <td>Pembina County Memorial Hospital</td>
            <td>Cavalier</td>
            <td>ND</td>
            <td>3544.0</td>
        </tr>
        <tr>
            <td>Pocahontas Community Hospital</td>
            <td>Pocahontas</td>
            <td>IA</td>
            <td>3545.0</td>
        </tr>
        <tr>
            <td>Sarah D. Culbertson Memorial Hospital</td>
            <td>Rushville</td>
            <td>IL</td>
            <td>3546.0</td>
        </tr>
        <tr>
            <td>Hamilton Memorial Hospital District</td>
            <td>McLeansboro</td>
            <td>IL</td>
            <td>3547.0</td>
        </tr>
        <tr>
            <td>Iron County Medical Center</td>
            <td>Pilot Knob</td>
            <td>MO</td>
            <td>3548.0</td>
        </tr>
        <tr>
            <td>Jefferson County Health Center</td>
            <td>Fairfield</td>
            <td>IA</td>
            <td>3549.0</td>
        </tr>
        <tr>
            <td>Gibson General Hospital</td>
            <td>Princeton</td>
            <td>IN</td>
            <td>3550.0</td>
        </tr>
        <tr>
            <td>Unity Medical Center</td>
            <td>Grafton</td>
            <td>ND</td>
            <td>3551.0</td>
        </tr>
        <tr>
            <td>Callaway District Hospital</td>
            <td>Callaway</td>
            <td>NE</td>
            <td>3552.0</td>
        </tr>
        <tr>
            <td>Cook Medical CenterÂ¬â€ a Campus of Tift Reg Medical Center</td>
            <td>Adel</td>
            <td>GA</td>
            <td>3553.0</td>
        </tr>
        <tr>
            <td>Ephraim Mcdowell Fort Logan Hospital</td>
            <td>Stanford</td>
            <td>KY</td>
            <td>3555.0</td>
        </tr>
        <tr>
            <td>Gundersen Palmer Lutheran Hospital and Clinics</td>
            <td>West Union</td>
            <td>IA</td>
            <td>3556.0</td>
        </tr>
        <tr>
            <td>Sequoyah County-City of Sallisaw Hospital Authorit</td>
            <td>Sallisaw</td>
            <td>OK</td>
            <td>3557.0</td>
        </tr>
        <tr>
            <td>O&#x27;Connor Hospital</td>
            <td>Delhi</td>
            <td>NY</td>
            <td>3559.0</td>
        </tr>
        <tr>
            <td>Grace Cottage Hospital</td>
            <td>Townshend</td>
            <td>VT</td>
            <td>3560.0</td>
        </tr>
        <tr>
            <td>Bowdle Hospital - CAH</td>
            <td>Bowdle</td>
            <td>SD</td>
            <td>3561.0</td>
        </tr>
        <tr>
            <td>Tyler Holmes Memorial Hospital</td>
            <td>Winona</td>
            <td>MS</td>
            <td>3562.0</td>
        </tr>
        <tr>
            <td>Veterans Memorial Hospital</td>
            <td>Waukon</td>
            <td>IA</td>
            <td>3563.0</td>
        </tr>
        <tr>
            <td>Magee General Hospital</td>
            <td>Magee</td>
            <td>MS</td>
            <td>3564.0</td>
        </tr>
        <tr>
            <td>Five Rivers Medical Center</td>
            <td>Pocahontas</td>
            <td>AR</td>
            <td>3565.0</td>
        </tr>
        <tr>
            <td>Fredonia Regional Hospital</td>
            <td>Fredonia</td>
            <td>KS</td>
            <td>3566.0</td>
        </tr>
        <tr>
            <td>Beaver Valley Hospital</td>
            <td>Beaver</td>
            <td>UT</td>
            <td>3567.0</td>
        </tr>
        <tr>
            <td>Anthony Medical Center</td>
            <td>Anthony</td>
            <td>KS</td>
            <td>3568.0</td>
        </tr>
        <tr>
            <td>Mckenzie Health System</td>
            <td>Sandusky</td>
            <td>MI</td>
            <td>3569.0</td>
        </tr>
        <tr>
            <td>Eastern Oklahoma Medical Center</td>
            <td>Poteau</td>
            <td>OK</td>
            <td>3571.0</td>
        </tr>
        <tr>
            <td>Sleepy Eye Municipal Hospital</td>
            <td>Sleepy Eye</td>
            <td>MN</td>
            <td>3572.0</td>
        </tr>
        <tr>
            <td>Humboldt County Memorial Hospital</td>
            <td>Humboldt</td>
            <td>IA</td>
            <td>3573.0</td>
        </tr>
        <tr>
            <td>Cedar County Memorial Hospital</td>
            <td>El Dorado Springs</td>
            <td>MO</td>
            <td>3574.0</td>
        </tr>
        <tr>
            <td>George C Grape Community Hospital</td>
            <td>Hamburg</td>
            <td>IA</td>
            <td>3575.0</td>
        </tr>
        <tr>
            <td>Stewart Memorial Community Hospital</td>
            <td>Lake City</td>
            <td>IA</td>
            <td>3576.0</td>
        </tr>
        <tr>
            <td>Community Memorial Hospital</td>
            <td>Staunton</td>
            <td>IL</td>
            <td>3577.0</td>
        </tr>
        <tr>
            <td>Cheyenne County Hospital</td>
            <td>St. Francis</td>
            <td>KS</td>
            <td>3579.0</td>
        </tr>
        <tr>
            <td>Atoka County Medical Center</td>
            <td>Atoka</td>
            <td>OK</td>
            <td>3580.0</td>
        </tr>
        <tr>
            <td>Okeene Municipal Hospital</td>
            <td>Okeene</td>
            <td>OK</td>
            <td>3581.0</td>
        </tr>
        <tr>
            <td>Jackson Medical Center</td>
            <td>Jackson</td>
            <td>AL</td>
            <td>3582.0</td>
        </tr>
        <tr>
            <td>Franklin County Memorial Hospital</td>
            <td>Meadville</td>
            <td>MS</td>
            <td>3583.0</td>
        </tr>
        <tr>
            <td>Minneola District Hospital Nbr 2</td>
            <td>Minneola</td>
            <td>KS</td>
            <td>3584.0</td>
        </tr>
        <tr>
            <td>West Holt Memorial Hospital</td>
            <td>Atkinson</td>
            <td>NE</td>
            <td>3585.0</td>
        </tr>
        <tr>
            <td>Izard County Medical Center, Llc</td>
            <td>Calico Rock</td>
            <td>AR</td>
            <td>3586.0</td>
        </tr>
        <tr>
            <td>Ellinwood District Hospital</td>
            <td>Ellinwood</td>
            <td>KS</td>
            <td>3587.0</td>
        </tr>
        <tr>
            <td>Putnam General Hospital</td>
            <td>Eatonton</td>
            <td>GA</td>
            <td>3588.0</td>
        </tr>
        <tr>
            <td>Holdenville General Hospital</td>
            <td>Holdenville</td>
            <td>OK</td>
            <td>3589.0</td>
        </tr>
        <tr>
            <td>Sullivan County Memorial Hospital</td>
            <td>Milan</td>
            <td>MO</td>
            <td>3590.0</td>
        </tr>
        <tr>
            <td>McGehee Hospital</td>
            <td>McGehee</td>
            <td>AR</td>
            <td>3591.0</td>
        </tr>
        <tr>
            <td>Caldwell Medical Center</td>
            <td>Princeton</td>
            <td>KY</td>
            <td>3592.0</td>
        </tr>
        <tr>
            <td>Norton County Hospital</td>
            <td>Norton</td>
            <td>KS</td>
            <td>3593.0</td>
        </tr>
        <tr>
            <td>Prairie Ridge Hospital And Health Services</td>
            <td>Elbow Lake</td>
            <td>MN</td>
            <td>3594.0</td>
        </tr>
        <tr>
            <td>First Care Health Center</td>
            <td>Park River</td>
            <td>ND</td>
            <td>3595.0</td>
        </tr>
        <tr>
            <td>Kane County Hospital</td>
            <td>Kanab</td>
            <td>UT</td>
            <td>3596.0</td>
        </tr>
        <tr>
            <td>Share Medical Center</td>
            <td>Alva</td>
            <td>OK</td>
            <td>3597.0</td>
        </tr>
        <tr>
            <td>Medicine Lodge Memorial Hospital</td>
            <td>Medicine Lodge</td>
            <td>KS</td>
            <td>3598.0</td>
        </tr>
        <tr>
            <td>Carnegie Tri-County Municipal Hospital</td>
            <td>Carnegie</td>
            <td>OK</td>
            <td>3599.0</td>
        </tr>
        <tr>
            <td>Hospital District #1 of Rice County</td>
            <td>Lyons</td>
            <td>KS</td>
            <td>3600.0</td>
        </tr>
        <tr>
            <td>Alliance Healthcare System</td>
            <td>Holly Springs</td>
            <td>MS</td>
            <td>3601.0</td>
        </tr>
        <tr>
            <td>Covington County Hospital Cah</td>
            <td>Collins</td>
            <td>MS</td>
            <td>3602.0</td>
        </tr>
        <tr>
            <td>Seiling Municipal Hospital</td>
            <td>Seiling</td>
            <td>OK</td>
            <td>3603.0</td>
        </tr>
        <tr>
            <td>Harper County Community Hospital</td>
            <td>Buffalo</td>
            <td>OK</td>
            <td>3604.0</td>
        </tr>
        <tr>
            <td>The Physicians&#x27; Hospital in Anadarko</td>
            <td>Anadarko</td>
            <td>OK</td>
            <td>3605.0</td>
        </tr>
        <tr>
            <td>Lifebrite Community Hospital Of Early</td>
            <td>Blakely</td>
            <td>GA</td>
            <td>3606.0</td>
        </tr>
    </tbody>
</table>



 

Q5. How many hospitals have an inclusivity rank in the top 25%?


```sql
%%sql
SELECT Name
    , City
    , State
    , [Tier 3_Inclusivity Rank] AS 'Inclusivity Rank'
FROM hospital_ranking
WHERE [Tier 3_Inclusivity Rank] IS NOT NULL
ORDER BY [Tier 3_Inclusivity Rank]
LIMIT (SELECT ROUND((COUNT(Name) * 0.25)) FROM hospital_ranking WHERE [Tier 3_Inclusivity Rank] IS NOT NULL)
;
    
```

     * sqlite:///lown_hospital.db
    Done.
    




<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>City</th>
            <th>State</th>
            <th>Inclusivity Rank</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Lakeside Medical Center</td>
            <td>Belle Glade</td>
            <td>FL</td>
            <td>1.0</td>
        </tr>
        <tr>
            <td>Truman Medical Centers</td>
            <td>None</td>
            <td>MO</td>
            <td>1.0</td>
        </tr>
        <tr>
            <td>Metropolitan Hospital Center</td>
            <td>New York</td>
            <td>NY</td>
            <td>2.0</td>
        </tr>
        <tr>
            <td>Archbold Medical Center</td>
            <td>None</td>
            <td>GA</td>
            <td>2.0</td>
        </tr>
        <tr>
            <td>Lincoln Medical &amp; Mental Health Center</td>
            <td>Bronx</td>
            <td>NY</td>
            <td>3.0</td>
        </tr>
        <tr>
            <td>Astria Health</td>
            <td>None</td>
            <td>WA</td>
            <td>3.0</td>
        </tr>
        <tr>
            <td>Boston Medical Center Corporation</td>
            <td>Boston</td>
            <td>MA</td>
            <td>4.0</td>
        </tr>
        <tr>
            <td>Maury Regional Medical Center</td>
            <td>None</td>
            <td>TN</td>
            <td>4.0</td>
        </tr>
        <tr>
            <td>Carepoint Health-Hoboken University Medical Center</td>
            <td>Hoboken</td>
            <td>NJ</td>
            <td>5.0</td>
        </tr>
        <tr>
            <td>Sinai Chicago</td>
            <td>None</td>
            <td>IL</td>
            <td>5.0</td>
        </tr>
        <tr>
            <td>Howard University Hospital</td>
            <td>Washington</td>
            <td>DC</td>
            <td>6.0</td>
        </tr>
        <tr>
            <td>Los Angeles County Health Services Department</td>
            <td>None</td>
            <td>CA</td>
            <td>6.0</td>
        </tr>
        <tr>
            <td>Truman Medical Center Hospital Hill</td>
            <td>Kansas City</td>
            <td>MO</td>
            <td>7.0</td>
        </tr>
        <tr>
            <td>Ephraim Mcdowell Health</td>
            <td>None</td>
            <td>KY</td>
            <td>7.0</td>
        </tr>
        <tr>
            <td>Mt. Sinai Hospital Medical Center</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>8.0</td>
        </tr>
        <tr>
            <td>Central Maine Healthcare</td>
            <td>None</td>
            <td>ME</td>
            <td>8.0</td>
        </tr>
        <tr>
            <td>Loretto Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>9.0</td>
        </tr>
        <tr>
            <td>Adventist Healthcare</td>
            <td>None</td>
            <td>MD</td>
            <td>9.0</td>
        </tr>
        <tr>
            <td>Adventist Healthcare</td>
            <td>None</td>
            <td>DC</td>
            <td>9.0</td>
        </tr>
        <tr>
            <td>Harlem Hospital Center</td>
            <td>New York</td>
            <td>NY</td>
            <td>10.0</td>
        </tr>
        <tr>
            <td>CentraCare Health System</td>
            <td>None</td>
            <td>MN</td>
            <td>10.0</td>
        </tr>
        <tr>
            <td>Methodist Dallas Medical Center</td>
            <td>Dallas</td>
            <td>TX</td>
            <td>11.0</td>
        </tr>
        <tr>
            <td>Valley Health System</td>
            <td>None</td>
            <td>VA</td>
            <td>11.0</td>
        </tr>
        <tr>
            <td>Valley Health System</td>
            <td>None</td>
            <td>WV</td>
            <td>11.0</td>
        </tr>
        <tr>
            <td>John H. Stroger Jr. Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>12.0</td>
        </tr>
        <tr>
            <td>University of Chicago Medicine</td>
            <td>None</td>
            <td>IL</td>
            <td>12.0</td>
        </tr>
        <tr>
            <td>Metro Nashville General Hospital</td>
            <td>Nashville</td>
            <td>TN</td>
            <td>13.0</td>
        </tr>
        <tr>
            <td>Einstein Healthcare Network</td>
            <td>None</td>
            <td>PA</td>
            <td>13.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital and Medical Center</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>14.0</td>
        </tr>
        <tr>
            <td>Saint Josephs Candler Health System</td>
            <td>None</td>
            <td>GA</td>
            <td>14.0</td>
        </tr>
        <tr>
            <td>University of Maryland Medical Center Midtown Campus</td>
            <td>Baltimore</td>
            <td>MD</td>
            <td>15.0</td>
        </tr>
        <tr>
            <td>VCU Health System</td>
            <td>None</td>
            <td>VA</td>
            <td>15.0</td>
        </tr>
        <tr>
            <td>Saint Anthony Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>16.0</td>
        </tr>
        <tr>
            <td>Ridgeview Medical Center</td>
            <td>None</td>
            <td>MN</td>
            <td>16.0</td>
        </tr>
        <tr>
            <td>Palisades Medical Center</td>
            <td>North Bergen</td>
            <td>NJ</td>
            <td>17.0</td>
        </tr>
        <tr>
            <td>Capital Health System</td>
            <td>None</td>
            <td>NJ</td>
            <td>17.0</td>
        </tr>
        <tr>
            <td>United Medical Center</td>
            <td>Washington</td>
            <td>DC</td>
            <td>18.0</td>
        </tr>
        <tr>
            <td>Infirmary Health System</td>
            <td>None</td>
            <td>AL</td>
            <td>18.0</td>
        </tr>
        <tr>
            <td>Norwegian-American Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>19.0</td>
        </tr>
        <tr>
            <td>MedStar Health</td>
            <td>None</td>
            <td>DC</td>
            <td>19.0</td>
        </tr>
        <tr>
            <td>MedStar Health</td>
            <td>None</td>
            <td>MD</td>
            <td>19.0</td>
        </tr>
        <tr>
            <td>St. Joseph Medical Center</td>
            <td>Houston</td>
            <td>TX</td>
            <td>20.0</td>
        </tr>
        <tr>
            <td>SoutheastHEALTH</td>
            <td>None</td>
            <td>MO</td>
            <td>20.0</td>
        </tr>
        <tr>
            <td>University Hospital</td>
            <td>Newark</td>
            <td>NJ</td>
            <td>21.0</td>
        </tr>
        <tr>
            <td>DCH Health System</td>
            <td>None</td>
            <td>AL</td>
            <td>21.0</td>
        </tr>
        <tr>
            <td>Southwest General Hospital</td>
            <td>San Antonio</td>
            <td>TX</td>
            <td>22.0</td>
        </tr>
        <tr>
            <td>Presbyterian Healthcare Services</td>
            <td>None</td>
            <td>NM</td>
            <td>22.0</td>
        </tr>
        <tr>
            <td>Parkland Health and Hospital System</td>
            <td>Dallas</td>
            <td>TX</td>
            <td>23.0</td>
        </tr>
        <tr>
            <td>Washington Health System</td>
            <td>None</td>
            <td>PA</td>
            <td>23.0</td>
        </tr>
        <tr>
            <td>Colleton Medical Center</td>
            <td>Walterboro</td>
            <td>SC</td>
            <td>24.0</td>
        </tr>
        <tr>
            <td>Garnet Health</td>
            <td>None</td>
            <td>NY</td>
            <td>24.0</td>
        </tr>
        <tr>
            <td>Medstar Washington Hospital Center</td>
            <td>Washington</td>
            <td>DC</td>
            <td>25.0</td>
        </tr>
        <tr>
            <td>Avanti Hospitals</td>
            <td>None</td>
            <td>CA</td>
            <td>25.0</td>
        </tr>
        <tr>
            <td>University of Illinois Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>26.0</td>
        </tr>
        <tr>
            <td>Lee Health</td>
            <td>None</td>
            <td>FL</td>
            <td>26.0</td>
        </tr>
        <tr>
            <td>Parkview Medical Center</td>
            <td>Pueblo</td>
            <td>CO</td>
            <td>27.0</td>
        </tr>
        <tr>
            <td>NYC Health + Hospitals</td>
            <td>None</td>
            <td>NY</td>
            <td>27.0</td>
        </tr>
        <tr>
            <td>Presence Saints Mary and Elizabeth Medical Center</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>28.0</td>
        </tr>
        <tr>
            <td>ThedaCare</td>
            <td>None</td>
            <td>WI</td>
            <td>28.0</td>
        </tr>
        <tr>
            <td>United Memorial Medical Center</td>
            <td>Houston</td>
            <td>TX</td>
            <td>29.0</td>
        </tr>
        <tr>
            <td>Mosaic Life Care</td>
            <td>None</td>
            <td>MO</td>
            <td>29.0</td>
        </tr>
        <tr>
            <td>Madera Community Hospital</td>
            <td>Madera</td>
            <td>CA</td>
            <td>30.0</td>
        </tr>
        <tr>
            <td>Methodist Health System</td>
            <td>None</td>
            <td>TX</td>
            <td>30.0</td>
        </tr>
        <tr>
            <td>Maury Regional Hospital</td>
            <td>Columbia</td>
            <td>TN</td>
            <td>31.0</td>
        </tr>
        <tr>
            <td>Alameda Health System</td>
            <td>None</td>
            <td>CA</td>
            <td>31.0</td>
        </tr>
        <tr>
            <td>Centura Health-St. Mary Corwin Medical Center</td>
            <td>Pueblo</td>
            <td>CO</td>
            <td>32.0</td>
        </tr>
        <tr>
            <td>Rochester Regional Health System</td>
            <td>None</td>
            <td>NY</td>
            <td>32.0</td>
        </tr>
        <tr>
            <td>St. Charles Madras</td>
            <td>Madras</td>
            <td>OR</td>
            <td>33.0</td>
        </tr>
        <tr>
            <td>Mary Washington Healthcare</td>
            <td>None</td>
            <td>VA</td>
            <td>33.0</td>
        </tr>
        <tr>
            <td>Beatrice Community Hospital &amp; Health Center</td>
            <td>Beatrice</td>
            <td>NE</td>
            <td>34.0</td>
        </tr>
        <tr>
            <td>UMass Memorial Health Care</td>
            <td>None</td>
            <td>MA</td>
            <td>34.0</td>
        </tr>
        <tr>
            <td>LAC+USC Medical Center</td>
            <td>Los Angeles</td>
            <td>CA</td>
            <td>35.0</td>
        </tr>
        <tr>
            <td>Tufts Medicine</td>
            <td>None</td>
            <td>MA</td>
            <td>35.0</td>
        </tr>
        <tr>
            <td>Hialeah Hospital</td>
            <td>Hialeah</td>
            <td>FL</td>
            <td>36.0</td>
        </tr>
        <tr>
            <td>Guthrie Clinic</td>
            <td>None</td>
            <td>NY</td>
            <td>36.0</td>
        </tr>
        <tr>
            <td>Guthrie Clinic</td>
            <td>None</td>
            <td>PA</td>
            <td>36.0</td>
        </tr>
        <tr>
            <td>Grady Memorial Hospital</td>
            <td>Atlanta</td>
            <td>GA</td>
            <td>37.0</td>
        </tr>
        <tr>
            <td>Centra Health</td>
            <td>None</td>
            <td>VA</td>
            <td>37.0</td>
        </tr>
        <tr>
            <td>Vista Medical Center East</td>
            <td>Waukegan</td>
            <td>IL</td>
            <td>38.0</td>
        </tr>
        <tr>
            <td>SSM Health</td>
            <td>None</td>
            <td>MO</td>
            <td>38.0</td>
        </tr>
        <tr>
            <td>SSM Health</td>
            <td>None</td>
            <td>IL</td>
            <td>38.0</td>
        </tr>
        <tr>
            <td>SSM Health</td>
            <td>None</td>
            <td>WI</td>
            <td>38.0</td>
        </tr>
        <tr>
            <td>SSM Health</td>
            <td>None</td>
            <td>OK</td>
            <td>38.0</td>
        </tr>
        <tr>
            <td>Marcum &amp; Wallace Memorial Hospital</td>
            <td>Irvine</td>
            <td>KY</td>
            <td>39.0</td>
        </tr>
        <tr>
            <td>Monument Health</td>
            <td>None</td>
            <td>SD</td>
            <td>39.0</td>
        </tr>
        <tr>
            <td>Banner-University Medical Center South Campus</td>
            <td>Tucson</td>
            <td>AZ</td>
            <td>40.0</td>
        </tr>
        <tr>
            <td>Spartanburg Regional Healthcare System</td>
            <td>None</td>
            <td>SC</td>
            <td>40.0</td>
        </tr>
        <tr>
            <td>Missouri Baptist Sullivan Hospital</td>
            <td>Sullivan</td>
            <td>MO</td>
            <td>41.0</td>
        </tr>
        <tr>
            <td>North Memorial Health Care</td>
            <td>None</td>
            <td>MN</td>
            <td>41.0</td>
        </tr>
        <tr>
            <td>White Memorial Medical Center</td>
            <td>Los Angeles</td>
            <td>CA</td>
            <td>42.0</td>
        </tr>
        <tr>
            <td>University of Missouri Health Care</td>
            <td>None</td>
            <td>MO</td>
            <td>42.0</td>
        </tr>
        <tr>
            <td>North Vista Hospital</td>
            <td>North Las Vegas</td>
            <td>NV</td>
            <td>43.0</td>
        </tr>
        <tr>
            <td>Carepoint Health</td>
            <td>None</td>
            <td>NJ</td>
            <td>43.0</td>
        </tr>
        <tr>
            <td>Clark Regional Medical Center</td>
            <td>Winchester</td>
            <td>KY</td>
            <td>44.0</td>
        </tr>
        <tr>
            <td>Erlanger Health System</td>
            <td>None</td>
            <td>NC</td>
            <td>44.0</td>
        </tr>
        <tr>
            <td>Erlanger Health System</td>
            <td>None</td>
            <td>TN</td>
            <td>44.0</td>
        </tr>
        <tr>
            <td>CHI St. Vincent Morrilton</td>
            <td>Morrilton</td>
            <td>AR</td>
            <td>45.0</td>
        </tr>
        <tr>
            <td>North Mississippi Health Services</td>
            <td>None</td>
            <td>AL</td>
            <td>45.0</td>
        </tr>
        <tr>
            <td>North Mississippi Health Services</td>
            <td>None</td>
            <td>MS</td>
            <td>45.0</td>
        </tr>
        <tr>
            <td>Salinas Valley Memorial Hospital</td>
            <td>Salinas</td>
            <td>CA</td>
            <td>46.0</td>
        </tr>
        <tr>
            <td>Vidant Health</td>
            <td>None</td>
            <td>NC</td>
            <td>46.0</td>
        </tr>
        <tr>
            <td>Sunnyside Community Hospital</td>
            <td>Sunnyside</td>
            <td>WA</td>
            <td>47.0</td>
        </tr>
        <tr>
            <td>West Tennessee Healthcare</td>
            <td>None</td>
            <td>TN</td>
            <td>47.0</td>
        </tr>
        <tr>
            <td>Woodhull Medical and Mental Health Center</td>
            <td>Brooklyn</td>
            <td>NY</td>
            <td>48.0</td>
        </tr>
        <tr>
            <td>Berkshire Health Systems</td>
            <td>None</td>
            <td>MA</td>
            <td>48.0</td>
        </tr>
        <tr>
            <td>Cambridge Health Alliance</td>
            <td>Cambridge</td>
            <td>MA</td>
            <td>49.0</td>
        </tr>
        <tr>
            <td>Inspira Health Network</td>
            <td>None</td>
            <td>NJ</td>
            <td>49.0</td>
        </tr>
        <tr>
            <td>Carney Hospital</td>
            <td>Boston</td>
            <td>MA</td>
            <td>50.0</td>
        </tr>
        <tr>
            <td>Heywood Healthcare</td>
            <td>None</td>
            <td>MA</td>
            <td>50.0</td>
        </tr>
        <tr>
            <td>Central Maine Medical Center</td>
            <td>Lewiston</td>
            <td>ME</td>
            <td>51.0</td>
        </tr>
        <tr>
            <td>Northern Arizona Healthcare</td>
            <td>None</td>
            <td>AZ</td>
            <td>51.0</td>
        </tr>
        <tr>
            <td>Bronx-Lebanon Hospital Center</td>
            <td>Bronx</td>
            <td>NY</td>
            <td>52.0</td>
        </tr>
        <tr>
            <td>Heritage Valley Health System</td>
            <td>None</td>
            <td>PA</td>
            <td>52.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Elmore Medical Center</td>
            <td>Mountain Home</td>
            <td>ID</td>
            <td>53.0</td>
        </tr>
        <tr>
            <td>Lehigh Valley Health Network</td>
            <td>None</td>
            <td>PA</td>
            <td>53.0</td>
        </tr>
        <tr>
            <td>Field Health System</td>
            <td>Centreville</td>
            <td>MS</td>
            <td>54.0</td>
        </tr>
        <tr>
            <td>Tower Health</td>
            <td>None</td>
            <td>PA</td>
            <td>54.0</td>
        </tr>
        <tr>
            <td>Harris Health System</td>
            <td>Houston</td>
            <td>TX</td>
            <td>55.0</td>
        </tr>
        <tr>
            <td>Commonwealth Health Corporation</td>
            <td>None</td>
            <td>KY</td>
            <td>55.0</td>
        </tr>
        <tr>
            <td>Regional Medical Center of San Jose</td>
            <td>San Jose</td>
            <td>CA</td>
            <td>56.0</td>
        </tr>
        <tr>
            <td>Freeman Health System</td>
            <td>None</td>
            <td>MO</td>
            <td>56.0</td>
        </tr>
        <tr>
            <td>Grady Memorial Hospital</td>
            <td>Chickasha</td>
            <td>OK</td>
            <td>57.0</td>
        </tr>
        <tr>
            <td>Northern Light Health</td>
            <td>None</td>
            <td>ME</td>
            <td>57.0</td>
        </tr>
        <tr>
            <td>Chinese Hospital</td>
            <td>San Francisco</td>
            <td>CA</td>
            <td>58.0</td>
        </tr>
        <tr>
            <td>Baylor Scott &amp; White Health</td>
            <td>None</td>
            <td>TX</td>
            <td>58.0</td>
        </tr>
        <tr>
            <td>Three Rivers Medical Center</td>
            <td>Louisa</td>
            <td>KY</td>
            <td>59.0</td>
        </tr>
        <tr>
            <td>Ballad Health</td>
            <td>None</td>
            <td>TN</td>
            <td>59.0</td>
        </tr>
        <tr>
            <td>Ballad Health</td>
            <td>None</td>
            <td>VA</td>
            <td>59.0</td>
        </tr>
        <tr>
            <td>Granville Health Systems</td>
            <td>Oxford</td>
            <td>NC</td>
            <td>60.0</td>
        </tr>
        <tr>
            <td>Franciscan Sisters of Christian Charity Sponsored Ministries, Inc.</td>
            <td>None</td>
            <td>NE</td>
            <td>60.0</td>
        </tr>
        <tr>
            <td>Franciscan Sisters of Christian Charity Sponsored Ministries, Inc.</td>
            <td>None</td>
            <td>OH</td>
            <td>60.0</td>
        </tr>
        <tr>
            <td>Franciscan Sisters of Christian Charity Sponsored Ministries, Inc.</td>
            <td>None</td>
            <td>WI</td>
            <td>60.0</td>
        </tr>
        <tr>
            <td>Heber Valley Hospital</td>
            <td>Heber City</td>
            <td>UT</td>
            <td>61.0</td>
        </tr>
        <tr>
            <td>McLeod Health</td>
            <td>None</td>
            <td>SC</td>
            <td>61.0</td>
        </tr>
        <tr>
            <td>Wellstar Atlanta Medical Center</td>
            <td>Atlanta</td>
            <td>GA</td>
            <td>62.0</td>
        </tr>
        <tr>
            <td>Owensboro Health</td>
            <td>None</td>
            <td>KY</td>
            <td>62.0</td>
        </tr>
        <tr>
            <td>Temple University Hospital</td>
            <td>Philadelphia</td>
            <td>PA</td>
            <td>63.0</td>
        </tr>
        <tr>
            <td>University of Mississippi Health Care</td>
            <td>None</td>
            <td>MS</td>
            <td>63.0</td>
        </tr>
        <tr>
            <td>Tristar Horizon Medical Center</td>
            <td>Dickson</td>
            <td>TN</td>
            <td>64.0</td>
        </tr>
        <tr>
            <td>Rush University Health</td>
            <td>None</td>
            <td>IL</td>
            <td>64.0</td>
        </tr>
        <tr>
            <td>St. Cloud Hospital</td>
            <td>Saint Cloud</td>
            <td>MN</td>
            <td>65.0</td>
        </tr>
        <tr>
            <td>Steward Health Care System</td>
            <td>None</td>
            <td>FL</td>
            <td>65.0</td>
        </tr>
        <tr>
            <td>Steward Health Care System</td>
            <td>None</td>
            <td>LA</td>
            <td>65.0</td>
        </tr>
        <tr>
            <td>Steward Health Care System</td>
            <td>None</td>
            <td>AZ</td>
            <td>65.0</td>
        </tr>
        <tr>
            <td>Steward Health Care System</td>
            <td>None</td>
            <td>AR</td>
            <td>65.0</td>
        </tr>
        <tr>
            <td>Steward Health Care System</td>
            <td>None</td>
            <td>MA</td>
            <td>65.0</td>
        </tr>
        <tr>
            <td>Steward Health Care System</td>
            <td>None</td>
            <td>TX</td>
            <td>65.0</td>
        </tr>
        <tr>
            <td>Steward Health Care System</td>
            <td>None</td>
            <td>UT</td>
            <td>65.0</td>
        </tr>
        <tr>
            <td>Steward Health Care System</td>
            <td>None</td>
            <td>OH</td>
            <td>65.0</td>
        </tr>
        <tr>
            <td>Steward Health Care System</td>
            <td>None</td>
            <td>PA</td>
            <td>65.0</td>
        </tr>
        <tr>
            <td>Ozarks Community Hospital of Gravette</td>
            <td>Gravette</td>
            <td>AR</td>
            <td>66.0</td>
        </tr>
        <tr>
            <td>University Health Care System</td>
            <td>None</td>
            <td>GA</td>
            <td>66.0</td>
        </tr>
        <tr>
            <td>Fulton County Hospital</td>
            <td>Salem</td>
            <td>AR</td>
            <td>67.0</td>
        </tr>
        <tr>
            <td>Salina Regional Health Center</td>
            <td>None</td>
            <td>KS</td>
            <td>67.0</td>
        </tr>
        <tr>
            <td>Henry Ford Hospital</td>
            <td>Detroit</td>
            <td>MI</td>
            <td>68.0</td>
        </tr>
        <tr>
            <td>Southeast Georgia Health System</td>
            <td>None</td>
            <td>GA</td>
            <td>68.0</td>
        </tr>
        <tr>
            <td>Carepoint Health-Christ Hospital</td>
            <td>Jersey City</td>
            <td>NJ</td>
            <td>69.0</td>
        </tr>
        <tr>
            <td>Saint Francis Health System</td>
            <td>None</td>
            <td>OK</td>
            <td>69.0</td>
        </tr>
        <tr>
            <td>LAC/Olive View-UCLA Medical Center</td>
            <td>Sylmar</td>
            <td>CA</td>
            <td>70.0</td>
        </tr>
        <tr>
            <td>Adena Health System</td>
            <td>None</td>
            <td>OH</td>
            <td>70.0</td>
        </tr>
        <tr>
            <td>Clinton Memorial Hospital</td>
            <td>Wilmington</td>
            <td>OH</td>
            <td>71.0</td>
        </tr>
        <tr>
            <td>Palomar Health</td>
            <td>None</td>
            <td>CA</td>
            <td>71.0</td>
        </tr>
        <tr>
            <td>Baptist Health La Grange</td>
            <td>La Grange</td>
            <td>KY</td>
            <td>72.0</td>
        </tr>
        <tr>
            <td>Universal Health Services</td>
            <td>None</td>
            <td>FL</td>
            <td>72.0</td>
        </tr>
        <tr>
            <td>Universal Health Services</td>
            <td>None</td>
            <td>DC</td>
            <td>72.0</td>
        </tr>
        <tr>
            <td>Universal Health Services</td>
            <td>None</td>
            <td>CA</td>
            <td>72.0</td>
        </tr>
        <tr>
            <td>Universal Health Services</td>
            <td>None</td>
            <td>NV</td>
            <td>72.0</td>
        </tr>
        <tr>
            <td>Universal Health Services</td>
            <td>None</td>
            <td>TX</td>
            <td>72.0</td>
        </tr>
        <tr>
            <td>Universal Health Services</td>
            <td>None</td>
            <td>SC</td>
            <td>72.0</td>
        </tr>
        <tr>
            <td>Universal Health Services</td>
            <td>None</td>
            <td>OK</td>
            <td>72.0</td>
        </tr>
        <tr>
            <td>Pioneers Medical Center</td>
            <td>Meeker</td>
            <td>CO</td>
            <td>73.0</td>
        </tr>
        <tr>
            <td>Loma Linda University Adventist Health Sciences Center</td>
            <td>None</td>
            <td>CA</td>
            <td>73.0</td>
        </tr>
        <tr>
            <td>Brownfield Regional Medical Center</td>
            <td>Brownfield</td>
            <td>TX</td>
            <td>74.0</td>
        </tr>
        <tr>
            <td>Aultman Health Foundation</td>
            <td>None</td>
            <td>OH</td>
            <td>74.0</td>
        </tr>
        <tr>
            <td>Contra Costa Regional Medical Center</td>
            <td>Martinez</td>
            <td>CA</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>KY</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>KS</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>IA</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>MI</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>NV</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>MT</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>MS</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>AR</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>AZ</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>AL</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>CO</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>IN</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>ID</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>GA</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>VA</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>UT</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>TX</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>WA</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>WI</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>WY</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>WV</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>OK</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>OH</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>NM</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>OR</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>TN</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>SC</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Lifepoint Health</td>
            <td>None</td>
            <td>PA</td>
            <td>75.0</td>
        </tr>
        <tr>
            <td>Fountain Valley Regional Hospital &amp; Medical Center</td>
            <td>Fountain Valley</td>
            <td>CA</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Prime Healthcare Services</td>
            <td>None</td>
            <td>IN</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Prime Healthcare Services</td>
            <td>None</td>
            <td>KS</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Prime Healthcare Services</td>
            <td>None</td>
            <td>MI</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Prime Healthcare Services</td>
            <td>None</td>
            <td>GA</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Prime Healthcare Services</td>
            <td>None</td>
            <td>AL</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Prime Healthcare Services</td>
            <td>None</td>
            <td>CA</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Prime Healthcare Services</td>
            <td>None</td>
            <td>FL</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Prime Healthcare Services</td>
            <td>None</td>
            <td>PA</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Prime Healthcare Services</td>
            <td>None</td>
            <td>RI</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Prime Healthcare Services</td>
            <td>None</td>
            <td>TX</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Prime Healthcare Services</td>
            <td>None</td>
            <td>OH</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Prime Healthcare Services</td>
            <td>None</td>
            <td>MO</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Prime Healthcare Services</td>
            <td>None</td>
            <td>NV</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Prime Healthcare Services</td>
            <td>None</td>
            <td>NJ</td>
            <td>76.0</td>
        </tr>
        <tr>
            <td>Rollins Brook Community Hospital</td>
            <td>Lampasas</td>
            <td>TX</td>
            <td>77.0</td>
        </tr>
        <tr>
            <td>Finger Lakes Health</td>
            <td>None</td>
            <td>NY</td>
            <td>77.0</td>
        </tr>
        <tr>
            <td>University Hospital Mcduffie</td>
            <td>Thomson</td>
            <td>GA</td>
            <td>78.0</td>
        </tr>
        <tr>
            <td>UVA Health System</td>
            <td>None</td>
            <td>VA</td>
            <td>78.0</td>
        </tr>
        <tr>
            <td>JPS Health Network</td>
            <td>Fort Worth</td>
            <td>TX</td>
            <td>79.0</td>
        </tr>
        <tr>
            <td>PeaceHealth</td>
            <td>None</td>
            <td>AK</td>
            <td>79.0</td>
        </tr>
        <tr>
            <td>PeaceHealth</td>
            <td>None</td>
            <td>OR</td>
            <td>79.0</td>
        </tr>
        <tr>
            <td>PeaceHealth</td>
            <td>None</td>
            <td>WA</td>
            <td>79.0</td>
        </tr>
        <tr>
            <td>TRMC of Orangeburg &amp; Calhoun</td>
            <td>Orangeburg</td>
            <td>SC</td>
            <td>80.0</td>
        </tr>
        <tr>
            <td>Atrium Health</td>
            <td>None</td>
            <td>GA</td>
            <td>80.0</td>
        </tr>
        <tr>
            <td>Atrium Health</td>
            <td>None</td>
            <td>NC</td>
            <td>80.0</td>
        </tr>
        <tr>
            <td>Garden Grove Hospital &amp; Medical Center</td>
            <td>Garden Grove</td>
            <td>CA</td>
            <td>81.0</td>
        </tr>
        <tr>
            <td>Geisinger Health System</td>
            <td>None</td>
            <td>PA</td>
            <td>81.0</td>
        </tr>
        <tr>
            <td>SSM Health Saint Louis University Hospital</td>
            <td>Saint Louis</td>
            <td>MO</td>
            <td>82.0</td>
        </tr>
        <tr>
            <td>University of Vermont Health Network</td>
            <td>None</td>
            <td>NY</td>
            <td>82.0</td>
        </tr>
        <tr>
            <td>University of Vermont Health Network</td>
            <td>None</td>
            <td>VT</td>
            <td>82.0</td>
        </tr>
        <tr>
            <td>Lawnwood Regional Medical Center &amp; Heart Institute</td>
            <td>Fort Pierce</td>
            <td>FL</td>
            <td>83.0</td>
        </tr>
        <tr>
            <td>Premier Health</td>
            <td>None</td>
            <td>OH</td>
            <td>83.0</td>
        </tr>
        <tr>
            <td>Good Samaritan Hospital</td>
            <td>Los Angeles</td>
            <td>CA</td>
            <td>84.0</td>
        </tr>
        <tr>
            <td>Ochsner Health System</td>
            <td>None</td>
            <td>LA</td>
            <td>84.0</td>
        </tr>
        <tr>
            <td>Ochsner Health System</td>
            <td>None</td>
            <td>MS</td>
            <td>84.0</td>
        </tr>
        <tr>
            <td>George Washington University Hospital</td>
            <td>Washington</td>
            <td>DC</td>
            <td>85.0</td>
        </tr>
        <tr>
            <td>Rush Health Systems</td>
            <td>None</td>
            <td>MS</td>
            <td>85.0</td>
        </tr>
        <tr>
            <td>Androscoggin Valley Hospital</td>
            <td>Berlin</td>
            <td>NH</td>
            <td>86.0</td>
        </tr>
        <tr>
            <td>Forrest Health</td>
            <td>None</td>
            <td>MS</td>
            <td>86.0</td>
        </tr>
        <tr>
            <td>Raulerson Hospital</td>
            <td>Okeechobee</td>
            <td>FL</td>
            <td>87.0</td>
        </tr>
        <tr>
            <td>WellSpan Health</td>
            <td>None</td>
            <td>PA</td>
            <td>87.0</td>
        </tr>
        <tr>
            <td>Prosser Memorial Hospital</td>
            <td>Prosser</td>
            <td>WA</td>
            <td>88.0</td>
        </tr>
        <tr>
            <td>UF Health</td>
            <td>None</td>
            <td>FL</td>
            <td>88.0</td>
        </tr>
        <tr>
            <td>Hale County Hospital</td>
            <td>Greensboro</td>
            <td>AL</td>
            <td>89.0</td>
        </tr>
        <tr>
            <td>INTEGRIS Health</td>
            <td>None</td>
            <td>OK</td>
            <td>89.0</td>
        </tr>
        <tr>
            <td>Rockcastle Regional Hospital &amp; Respiratory Care Ct</td>
            <td>Mount Vernon</td>
            <td>KY</td>
            <td>90.0</td>
        </tr>
        <tr>
            <td>Excela Health</td>
            <td>None</td>
            <td>PA</td>
            <td>90.0</td>
        </tr>
        <tr>
            <td>New Orleans East Hospital</td>
            <td>New Orleans</td>
            <td>LA</td>
            <td>91.0</td>
        </tr>
        <tr>
            <td>University of Kansas Health System</td>
            <td>None</td>
            <td>KS</td>
            <td>91.0</td>
        </tr>
        <tr>
            <td>Toppenish Community Hospital</td>
            <td>Toppenish</td>
            <td>WA</td>
            <td>92.0</td>
        </tr>
        <tr>
            <td>Banner Health</td>
            <td>None</td>
            <td>CO</td>
            <td>92.0</td>
        </tr>
        <tr>
            <td>Banner Health</td>
            <td>None</td>
            <td>CA</td>
            <td>92.0</td>
        </tr>
        <tr>
            <td>Banner Health</td>
            <td>None</td>
            <td>AZ</td>
            <td>92.0</td>
        </tr>
        <tr>
            <td>Banner Health</td>
            <td>None</td>
            <td>WY</td>
            <td>92.0</td>
        </tr>
        <tr>
            <td>Banner Health</td>
            <td>None</td>
            <td>NV</td>
            <td>92.0</td>
        </tr>
        <tr>
            <td>Banner Health</td>
            <td>None</td>
            <td>NE</td>
            <td>92.0</td>
        </tr>
        <tr>
            <td>Uf Health Jacksonville</td>
            <td>Jacksonville</td>
            <td>FL</td>
            <td>93.0</td>
        </tr>
        <tr>
            <td>Baystate Health</td>
            <td>None</td>
            <td>MA</td>
            <td>93.0</td>
        </tr>
        <tr>
            <td>Albert Einstein Medical Center</td>
            <td>Philadelphia</td>
            <td>PA</td>
            <td>94.0</td>
        </tr>
        <tr>
            <td>Arnot Health</td>
            <td>None</td>
            <td>NY</td>
            <td>94.0</td>
        </tr>
        <tr>
            <td>Princeton Baptist Medical Center</td>
            <td>Birmingham</td>
            <td>AL</td>
            <td>95.0</td>
        </tr>
        <tr>
            <td>UAB Health System</td>
            <td>None</td>
            <td>AL</td>
            <td>95.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital of Gardena</td>
            <td>Gardena</td>
            <td>CA</td>
            <td>96.0</td>
        </tr>
        <tr>
            <td>Medisys Health Network</td>
            <td>None</td>
            <td>NY</td>
            <td>96.0</td>
        </tr>
        <tr>
            <td>Mission Community Hospital</td>
            <td>Panorama City</td>
            <td>CA</td>
            <td>97.0</td>
        </tr>
        <tr>
            <td>West Virginia University Health System</td>
            <td>None</td>
            <td>OH</td>
            <td>97.0</td>
        </tr>
        <tr>
            <td>West Virginia University Health System</td>
            <td>None</td>
            <td>MD</td>
            <td>97.0</td>
        </tr>
        <tr>
            <td>West Virginia University Health System</td>
            <td>None</td>
            <td>WV</td>
            <td>97.0</td>
        </tr>
        <tr>
            <td>West Virginia University Health System</td>
            <td>None</td>
            <td>PA</td>
            <td>97.0</td>
        </tr>
        <tr>
            <td>Miami County Medical Center</td>
            <td>Paola</td>
            <td>KS</td>
            <td>98.0</td>
        </tr>
        <tr>
            <td>SCL Health</td>
            <td>None</td>
            <td>CO</td>
            <td>98.0</td>
        </tr>
        <tr>
            <td>SCL Health</td>
            <td>None</td>
            <td>MT</td>
            <td>98.0</td>
        </tr>
        <tr>
            <td>City Hospital AtÂ¬â€  White Rock</td>
            <td>Dallas</td>
            <td>TX</td>
            <td>99.0</td>
        </tr>
        <tr>
            <td>Allina Health System</td>
            <td>None</td>
            <td>MN</td>
            <td>99.0</td>
        </tr>
        <tr>
            <td>Allina Health System</td>
            <td>None</td>
            <td>WI</td>
            <td>99.0</td>
        </tr>
        <tr>
            <td>Sweetwater Hospital Association</td>
            <td>Sweetwater</td>
            <td>TN</td>
            <td>100.0</td>
        </tr>
        <tr>
            <td>Duke LifePoint Healthcare</td>
            <td>None</td>
            <td>NC</td>
            <td>100.0</td>
        </tr>
        <tr>
            <td>Duke LifePoint Healthcare</td>
            <td>None</td>
            <td>MI</td>
            <td>100.0</td>
        </tr>
        <tr>
            <td>Duke LifePoint Healthcare</td>
            <td>None</td>
            <td>VA</td>
            <td>100.0</td>
        </tr>
        <tr>
            <td>Duke LifePoint Healthcare</td>
            <td>None</td>
            <td>PA</td>
            <td>100.0</td>
        </tr>
        <tr>
            <td>Saint Alphonsus Medical Center - Ontario</td>
            <td>Ontario</td>
            <td>OR</td>
            <td>101.0</td>
        </tr>
        <tr>
            <td>Mercy Health System</td>
            <td>None</td>
            <td>IL</td>
            <td>101.0</td>
        </tr>
        <tr>
            <td>Mercy Health System</td>
            <td>None</td>
            <td>WI</td>
            <td>101.0</td>
        </tr>
        <tr>
            <td>Abrazo Central Campus</td>
            <td>Phoenix</td>
            <td>AZ</td>
            <td>102.0</td>
        </tr>
        <tr>
            <td>Bronson Healthcare</td>
            <td>None</td>
            <td>MI</td>
            <td>102.0</td>
        </tr>
        <tr>
            <td>Arrowhead Regional Medical Center</td>
            <td>Colton</td>
            <td>CA</td>
            <td>103.0</td>
        </tr>
        <tr>
            <td>Appalachian Regional Healthcare</td>
            <td>None</td>
            <td>KY</td>
            <td>103.0</td>
        </tr>
        <tr>
            <td>Appalachian Regional Healthcare</td>
            <td>None</td>
            <td>WV</td>
            <td>103.0</td>
        </tr>
        <tr>
            <td>St. Barnabas Hospital</td>
            <td>Bronx</td>
            <td>NY</td>
            <td>104.0</td>
        </tr>
        <tr>
            <td>Methodist Le Bonheur Healthcare</td>
            <td>None</td>
            <td>MS</td>
            <td>104.0</td>
        </tr>
        <tr>
            <td>Methodist Le Bonheur Healthcare</td>
            <td>None</td>
            <td>TN</td>
            <td>104.0</td>
        </tr>
        <tr>
            <td>Avera Holy Family Hospital</td>
            <td>Estherville</td>
            <td>IA</td>
            <td>105.0</td>
        </tr>
        <tr>
            <td>Wakemed Health and Hospitals</td>
            <td>None</td>
            <td>NC</td>
            <td>105.0</td>
        </tr>
        <tr>
            <td>North Colorado Medical Center</td>
            <td>Greeley</td>
            <td>CO</td>
            <td>106.0</td>
        </tr>
        <tr>
            <td>Baptist Health</td>
            <td>None</td>
            <td>AR</td>
            <td>106.0</td>
        </tr>
        <tr>
            <td>LA Downtown Medical Center</td>
            <td>Los Angeles</td>
            <td>CA</td>
            <td>107.0</td>
        </tr>
        <tr>
            <td>Hendrick Health System</td>
            <td>None</td>
            <td>TX</td>
            <td>107.0</td>
        </tr>
        <tr>
            <td>Novant Health UVAÂ¬â€  Prince William Medical Center</td>
            <td>Manassas</td>
            <td>VA</td>
            <td>108.0</td>
        </tr>
        <tr>
            <td>ProMedica Health System</td>
            <td>None</td>
            <td>MI</td>
            <td>108.0</td>
        </tr>
        <tr>
            <td>ProMedica Health System</td>
            <td>None</td>
            <td>OH</td>
            <td>108.0</td>
        </tr>
        <tr>
            <td>Denver Health Medical Center</td>
            <td>Denver</td>
            <td>CO</td>
            <td>109.0</td>
        </tr>
        <tr>
            <td>Norton Healthcare</td>
            <td>None</td>
            <td>IN</td>
            <td>109.0</td>
        </tr>
        <tr>
            <td>Norton Healthcare</td>
            <td>None</td>
            <td>KY</td>
            <td>109.0</td>
        </tr>
        <tr>
            <td>West Valley Medical Center</td>
            <td>Caldwell</td>
            <td>ID</td>
            <td>110.0</td>
        </tr>
        <tr>
            <td>Southern Illinois Healthcare</td>
            <td>None</td>
            <td>IL</td>
            <td>110.0</td>
        </tr>
        <tr>
            <td>Hegg Memorial Health Center</td>
            <td>Rock Valley</td>
            <td>IA</td>
            <td>111.0</td>
        </tr>
        <tr>
            <td>Spectrum Health</td>
            <td>None</td>
            <td>MI</td>
            <td>111.0</td>
        </tr>
        <tr>
            <td>Starr County Memorial Hospital</td>
            <td>Rio Grande City</td>
            <td>TX</td>
            <td>112.0</td>
        </tr>
        <tr>
            <td>Nebraska Medicine</td>
            <td>None</td>
            <td>NE</td>
            <td>112.0</td>
        </tr>
        <tr>
            <td>Greater El Monte Community Hospital</td>
            <td>South El Monte</td>
            <td>CA</td>
            <td>113.0</td>
        </tr>
        <tr>
            <td>Holzer Health System</td>
            <td>None</td>
            <td>OH</td>
            <td>113.0</td>
        </tr>
        <tr>
            <td>Whitman Hospital and Medical Center</td>
            <td>Colfax</td>
            <td>WA</td>
            <td>114.0</td>
        </tr>
        <tr>
            <td>Prospect Medical Holdings</td>
            <td>None</td>
            <td>CT</td>
            <td>114.0</td>
        </tr>
        <tr>
            <td>Prospect Medical Holdings</td>
            <td>None</td>
            <td>CA</td>
            <td>114.0</td>
        </tr>
        <tr>
            <td>Prospect Medical Holdings</td>
            <td>None</td>
            <td>NJ</td>
            <td>114.0</td>
        </tr>
        <tr>
            <td>Prospect Medical Holdings</td>
            <td>None</td>
            <td>RI</td>
            <td>114.0</td>
        </tr>
        <tr>
            <td>Prospect Medical Holdings</td>
            <td>None</td>
            <td>PA</td>
            <td>114.0</td>
        </tr>
        <tr>
            <td>Sacred Heart Hospital</td>
            <td>Eau Claire</td>
            <td>WI</td>
            <td>115.0</td>
        </tr>
        <tr>
            <td>Genesis Health System</td>
            <td>None</td>
            <td>IL</td>
            <td>115.0</td>
        </tr>
        <tr>
            <td>Genesis Health System</td>
            <td>None</td>
            <td>IA</td>
            <td>115.0</td>
        </tr>
        <tr>
            <td>Capital Health Regional Medical Center</td>
            <td>Trenton</td>
            <td>NJ</td>
            <td>116.0</td>
        </tr>
        <tr>
            <td>Samaritan Health Services</td>
            <td>None</td>
            <td>OR</td>
            <td>116.0</td>
        </tr>
        <tr>
            <td>The University of Chicago Medical Center</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>117.0</td>
        </tr>
        <tr>
            <td>Sparrow Health System</td>
            <td>None</td>
            <td>MI</td>
            <td>117.0</td>
        </tr>
        <tr>
            <td>Park Plaza Hospital</td>
            <td>Houston</td>
            <td>TX</td>
            <td>118.0</td>
        </tr>
        <tr>
            <td>UCHealth (Colorado)</td>
            <td>None</td>
            <td>CO</td>
            <td>118.0</td>
        </tr>
        <tr>
            <td>Adventist Health and Rideout</td>
            <td>Marysville</td>
            <td>CA</td>
            <td>119.0</td>
        </tr>
        <tr>
            <td>Sanford Health</td>
            <td>None</td>
            <td>MN</td>
            <td>119.0</td>
        </tr>
        <tr>
            <td>Sanford Health</td>
            <td>None</td>
            <td>IA</td>
            <td>119.0</td>
        </tr>
        <tr>
            <td>Sanford Health</td>
            <td>None</td>
            <td>SD</td>
            <td>119.0</td>
        </tr>
        <tr>
            <td>Sanford Health</td>
            <td>None</td>
            <td>ND</td>
            <td>119.0</td>
        </tr>
        <tr>
            <td>Sutter Solano Medical Center</td>
            <td>Vallejo</td>
            <td>CA</td>
            <td>120.0</td>
        </tr>
        <tr>
            <td>Cox Health</td>
            <td>None</td>
            <td>MO</td>
            <td>120.0</td>
        </tr>
        <tr>
            <td>Banner Casa Grande Medical Center</td>
            <td>Casa Grande</td>
            <td>AZ</td>
            <td>121.0</td>
        </tr>
        <tr>
            <td>Essentia Health</td>
            <td>None</td>
            <td>MN</td>
            <td>121.0</td>
        </tr>
        <tr>
            <td>Essentia Health</td>
            <td>None</td>
            <td>ND</td>
            <td>121.0</td>
        </tr>
        <tr>
            <td>Essentia Health</td>
            <td>None</td>
            <td>WI</td>
            <td>121.0</td>
        </tr>
        <tr>
            <td>Doctors Medical Center</td>
            <td>Modesto</td>
            <td>CA</td>
            <td>122.0</td>
        </tr>
        <tr>
            <td>Huntsville Hospital Health System</td>
            <td>None</td>
            <td>AL</td>
            <td>122.0</td>
        </tr>
        <tr>
            <td>Emory University Hospital Midtown</td>
            <td>Atlanta</td>
            <td>GA</td>
            <td>123.0</td>
        </tr>
        <tr>
            <td>Saint Lukes Hospital of Duluth</td>
            <td>None</td>
            <td>MN</td>
            <td>123.0</td>
        </tr>
        <tr>
            <td>Lake View Memorial Hospital</td>
            <td>Two Harbors</td>
            <td>MN</td>
            <td>124.0</td>
        </tr>
        <tr>
            <td>Alecto Healthcare</td>
            <td>None</td>
            <td>CA</td>
            <td>124.0</td>
        </tr>
        <tr>
            <td>Alecto Healthcare</td>
            <td>None</td>
            <td>TX</td>
            <td>124.0</td>
        </tr>
        <tr>
            <td>Valley Presbyterian Hospital</td>
            <td>Van Nuys</td>
            <td>CA</td>
            <td>125.0</td>
        </tr>
        <tr>
            <td>Allegheny Health Network</td>
            <td>None</td>
            <td>PA</td>
            <td>125.0</td>
        </tr>
        <tr>
            <td>Paris Regional Medical Center</td>
            <td>Paris</td>
            <td>TX</td>
            <td>126.0</td>
        </tr>
        <tr>
            <td>Aspirus</td>
            <td>None</td>
            <td>MI</td>
            <td>126.0</td>
        </tr>
        <tr>
            <td>Aspirus</td>
            <td>None</td>
            <td>WI</td>
            <td>126.0</td>
        </tr>
        <tr>
            <td>Geisinger Medical Center</td>
            <td>Danville</td>
            <td>PA</td>
            <td>127.0</td>
        </tr>
        <tr>
            <td>Floyd Medical Center</td>
            <td>None</td>
            <td>GA</td>
            <td>127.0</td>
        </tr>
        <tr>
            <td>Redington Fairview General Hospital</td>
            <td>Skowhegan</td>
            <td>ME</td>
            <td>128.0</td>
        </tr>
        <tr>
            <td>St. Charles Health System</td>
            <td>None</td>
            <td>OR</td>
            <td>128.0</td>
        </tr>
        <tr>
            <td>SSM Health Depaul Hospital St. Louis</td>
            <td>Bridgeton</td>
            <td>MO</td>
            <td>129.0</td>
        </tr>
        <tr>
            <td>Gundersen Health System</td>
            <td>None</td>
            <td>IA</td>
            <td>129.0</td>
        </tr>
        <tr>
            <td>Gundersen Health System</td>
            <td>None</td>
            <td>MN</td>
            <td>129.0</td>
        </tr>
        <tr>
            <td>Gundersen Health System</td>
            <td>None</td>
            <td>WI</td>
            <td>129.0</td>
        </tr>
        <tr>
            <td>West Suburban Medical Center</td>
            <td>Oak Park</td>
            <td>IL</td>
            <td>130.0</td>
        </tr>
        <tr>
            <td>UC Health (Cincinnati)</td>
            <td>None</td>
            <td>OH</td>
            <td>130.0</td>
        </tr>
        <tr>
            <td>Newark Beth Israel Medical Center</td>
            <td>Newark</td>
            <td>NJ</td>
            <td>131.0</td>
        </tr>
        <tr>
            <td>Adventist Health</td>
            <td>None</td>
            <td>CA</td>
            <td>131.0</td>
        </tr>
        <tr>
            <td>Adventist Health</td>
            <td>None</td>
            <td>HI</td>
            <td>131.0</td>
        </tr>
        <tr>
            <td>Adventist Health</td>
            <td>None</td>
            <td>OR</td>
            <td>131.0</td>
        </tr>
        <tr>
            <td>University Hospital &amp; Clinics</td>
            <td>Lafayette</td>
            <td>LA</td>
            <td>132.0</td>
        </tr>
        <tr>
            <td>Mohawk Valley Health System</td>
            <td>None</td>
            <td>NY</td>
            <td>132.0</td>
        </tr>
        <tr>
            <td>Regional Health Sturgis Hospital</td>
            <td>Sturgis</td>
            <td>SD</td>
            <td>133.0</td>
        </tr>
        <tr>
            <td>Mercy Health</td>
            <td>None</td>
            <td>KY</td>
            <td>133.0</td>
        </tr>
        <tr>
            <td>Mercy Health</td>
            <td>None</td>
            <td>OH</td>
            <td>133.0</td>
        </tr>
        <tr>
            <td>Tidelands Health</td>
            <td>Georgetown</td>
            <td>SC</td>
            <td>134.0</td>
        </tr>
        <tr>
            <td>SolutioNHealth</td>
            <td>None</td>
            <td>NH</td>
            <td>134.0</td>
        </tr>
        <tr>
            <td>Newark-Wayne Community Hospital</td>
            <td>Newark</td>
            <td>NY</td>
            <td>135.0</td>
        </tr>
        <tr>
            <td>Sharp HealthCare</td>
            <td>None</td>
            <td>CA</td>
            <td>135.0</td>
        </tr>
        <tr>
            <td>Medstar Southern Maryland Hospital Center</td>
            <td>Clinton</td>
            <td>MD</td>
            <td>136.0</td>
        </tr>
        <tr>
            <td>Singing River Health System</td>
            <td>None</td>
            <td>MS</td>
            <td>136.0</td>
        </tr>
        <tr>
            <td>Harper University Hospital</td>
            <td>Detroit</td>
            <td>MI</td>
            <td>137.0</td>
        </tr>
        <tr>
            <td>Bon Secours Mercy Health System</td>
            <td>None</td>
            <td>OH</td>
            <td>137.0</td>
        </tr>
        <tr>
            <td>Bon Secours Mercy Health System</td>
            <td>None</td>
            <td>VA</td>
            <td>137.0</td>
        </tr>
        <tr>
            <td>Bon Secours Mercy Health System</td>
            <td>None</td>
            <td>SC</td>
            <td>137.0</td>
        </tr>
        <tr>
            <td>UofLÂ¬â€ Health - Jewish Hospital</td>
            <td>Louisville</td>
            <td>KY</td>
            <td>138.0</td>
        </tr>
        <tr>
            <td>Tanner Health System</td>
            <td>None</td>
            <td>GA</td>
            <td>138.0</td>
        </tr>
        <tr>
            <td>Winchester Medical Center</td>
            <td>Winchester</td>
            <td>VA</td>
            <td>139.0</td>
        </tr>
        <tr>
            <td>OSF Healthcare System</td>
            <td>None</td>
            <td>IL</td>
            <td>139.0</td>
        </tr>
        <tr>
            <td>OSF Healthcare System</td>
            <td>None</td>
            <td>MI</td>
            <td>139.0</td>
        </tr>
        <tr>
            <td>St. Mary&#x27;s Hospital at Amsterdam</td>
            <td>Amsterdam</td>
            <td>NY</td>
            <td>140.0</td>
        </tr>
        <tr>
            <td>Kootenai Health</td>
            <td>None</td>
            <td>ID</td>
            <td>140.0</td>
        </tr>
        <tr>
            <td>Merit Health Madison</td>
            <td>Canton</td>
            <td>MS</td>
            <td>141.0</td>
        </tr>
        <tr>
            <td>UW Medicine (Washington)</td>
            <td>None</td>
            <td>WA</td>
            <td>141.0</td>
        </tr>
        <tr>
            <td>Minden Medical Center</td>
            <td>Minden</td>
            <td>LA</td>
            <td>142.0</td>
        </tr>
        <tr>
            <td>United Health Services</td>
            <td>None</td>
            <td>NY</td>
            <td>142.0</td>
        </tr>
        <tr>
            <td>Osceola Medical Center</td>
            <td>Osceola</td>
            <td>WI</td>
            <td>143.0</td>
        </tr>
        <tr>
            <td>Lecom Health</td>
            <td>None</td>
            <td>PA</td>
            <td>143.0</td>
        </tr>
        <tr>
            <td>Los Angeles Community Hospital</td>
            <td>Los Angeles</td>
            <td>CA</td>
            <td>144.0</td>
        </tr>
        <tr>
            <td>St. Lukes University Health Network</td>
            <td>None</td>
            <td>NJ</td>
            <td>144.0</td>
        </tr>
        <tr>
            <td>St. Lukes University Health Network</td>
            <td>None</td>
            <td>PA</td>
            <td>144.0</td>
        </tr>
        <tr>
            <td>PeacHealth St. John Medical Center</td>
            <td>Longview</td>
            <td>WA</td>
            <td>145.0</td>
        </tr>
        <tr>
            <td>Hawaii Health Systems Corporation</td>
            <td>None</td>
            <td>HI</td>
            <td>145.0</td>
        </tr>
        <tr>
            <td>The Medical Center at Albany</td>
            <td>Albany</td>
            <td>KY</td>
            <td>146.0</td>
        </tr>
        <tr>
            <td>Ascension Healthcare</td>
            <td>None</td>
            <td>IN</td>
            <td>146.0</td>
        </tr>
        <tr>
            <td>Ascension Healthcare</td>
            <td>None</td>
            <td>KS</td>
            <td>146.0</td>
        </tr>
        <tr>
            <td>Ascension Healthcare</td>
            <td>None</td>
            <td>MD</td>
            <td>146.0</td>
        </tr>
        <tr>
            <td>Ascension Healthcare</td>
            <td>None</td>
            <td>AL</td>
            <td>146.0</td>
        </tr>
        <tr>
            <td>Ascension Healthcare</td>
            <td>None</td>
            <td>FL</td>
            <td>146.0</td>
        </tr>
        <tr>
            <td>Ascension Healthcare</td>
            <td>None</td>
            <td>IL</td>
            <td>146.0</td>
        </tr>
        <tr>
            <td>Ascension Healthcare</td>
            <td>None</td>
            <td>TN</td>
            <td>146.0</td>
        </tr>
        <tr>
            <td>Ascension Healthcare</td>
            <td>None</td>
            <td>TX</td>
            <td>146.0</td>
        </tr>
        <tr>
            <td>Ascension Healthcare</td>
            <td>None</td>
            <td>WI</td>
            <td>146.0</td>
        </tr>
        <tr>
            <td>Ascension Healthcare</td>
            <td>None</td>
            <td>MI</td>
            <td>146.0</td>
        </tr>
        <tr>
            <td>Ascension Healthcare</td>
            <td>None</td>
            <td>NY</td>
            <td>146.0</td>
        </tr>
        <tr>
            <td>Ascension Healthcare</td>
            <td>None</td>
            <td>OK</td>
            <td>146.0</td>
        </tr>
        <tr>
            <td>Champlain Valley Physicians Hospital Medical Center</td>
            <td>Plattsburgh</td>
            <td>NY</td>
            <td>147.0</td>
        </tr>
        <tr>
            <td>Beacon Health System</td>
            <td>None</td>
            <td>IN</td>
            <td>147.0</td>
        </tr>
        <tr>
            <td>Guadalupe Regional Medical Center</td>
            <td>Seguin</td>
            <td>TX</td>
            <td>148.0</td>
        </tr>
        <tr>
            <td>Union Health</td>
            <td>None</td>
            <td>IN</td>
            <td>148.0</td>
        </tr>
        <tr>
            <td>Adventist Bolingbrook Hospital</td>
            <td>Bolingbrook</td>
            <td>IL</td>
            <td>149.0</td>
        </tr>
        <tr>
            <td>WellStar Health System</td>
            <td>None</td>
            <td>GA</td>
            <td>149.0</td>
        </tr>
        <tr>
            <td>Thedacare Medical Center New London</td>
            <td>New London</td>
            <td>WI</td>
            <td>150.0</td>
        </tr>
        <tr>
            <td>South Georgia Medical Center</td>
            <td>None</td>
            <td>GA</td>
            <td>150.0</td>
        </tr>
        <tr>
            <td>Louis A. Weiss Memorial Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>151.0</td>
        </tr>
        <tr>
            <td>Henry Ford Health System</td>
            <td>None</td>
            <td>MI</td>
            <td>151.0</td>
        </tr>
        <tr>
            <td>Sinai-Grace Hospital</td>
            <td>Detroit</td>
            <td>MI</td>
            <td>152.0</td>
        </tr>
        <tr>
            <td>Unitypoint Health</td>
            <td>None</td>
            <td>IL</td>
            <td>152.0</td>
        </tr>
        <tr>
            <td>Unitypoint Health</td>
            <td>None</td>
            <td>IA</td>
            <td>152.0</td>
        </tr>
        <tr>
            <td>Unitypoint Health</td>
            <td>None</td>
            <td>WI</td>
            <td>152.0</td>
        </tr>
        <tr>
            <td>Baptist Health Richmond</td>
            <td>Richmond</td>
            <td>KY</td>
            <td>153.0</td>
        </tr>
        <tr>
            <td>Sutter Health</td>
            <td>None</td>
            <td>CA</td>
            <td>153.0</td>
        </tr>
        <tr>
            <td>Hollywood Presbyterian Medical Center</td>
            <td>Los Angeles</td>
            <td>CA</td>
            <td>154.0</td>
        </tr>
        <tr>
            <td>Indiana University Health</td>
            <td>None</td>
            <td>IN</td>
            <td>154.0</td>
        </tr>
        <tr>
            <td>Clay County Medical Center</td>
            <td>West Point</td>
            <td>MS</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>KS</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>ID</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>LA</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>KY</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>GA</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>CA</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>AK</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>FL</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>CO</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>MO</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>UT</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>TX</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>IN</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>VA</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>TN</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>NH</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>NV</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>SC</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>HCA Healthcare</td>
            <td>None</td>
            <td>NC</td>
            <td>155.0</td>
        </tr>
        <tr>
            <td>Hereford Regional Medical Center</td>
            <td>Hereford</td>
            <td>TX</td>
            <td>156.0</td>
        </tr>
        <tr>
            <td>Health First</td>
            <td>None</td>
            <td>FL</td>
            <td>156.0</td>
        </tr>
        <tr>
            <td>Saint Francis Hospital Muskogee</td>
            <td>Muskogee</td>
            <td>OK</td>
            <td>157.0</td>
        </tr>
        <tr>
            <td>MultiCare Health System</td>
            <td>None</td>
            <td>WA</td>
            <td>157.0</td>
        </tr>
        <tr>
            <td>Monroe County Hospital</td>
            <td>Forsyth</td>
            <td>GA</td>
            <td>158.0</td>
        </tr>
        <tr>
            <td>Barton Health</td>
            <td>None</td>
            <td>CA</td>
            <td>158.0</td>
        </tr>
        <tr>
            <td>Barton Health</td>
            <td>None</td>
            <td>NV</td>
            <td>158.0</td>
        </tr>
        <tr>
            <td>Carolinas Healthcare System Union</td>
            <td>Monroe</td>
            <td>NC</td>
            <td>159.0</td>
        </tr>
        <tr>
            <td>TENET Healthcare Corporation</td>
            <td>None</td>
            <td>CA</td>
            <td>159.0</td>
        </tr>
        <tr>
            <td>TENET Healthcare Corporation</td>
            <td>None</td>
            <td>FL</td>
            <td>159.0</td>
        </tr>
        <tr>
            <td>TENET Healthcare Corporation</td>
            <td>None</td>
            <td>AL</td>
            <td>159.0</td>
        </tr>
        <tr>
            <td>TENET Healthcare Corporation</td>
            <td>None</td>
            <td>AZ</td>
            <td>159.0</td>
        </tr>
        <tr>
            <td>TENET Healthcare Corporation</td>
            <td>None</td>
            <td>MA</td>
            <td>159.0</td>
        </tr>
        <tr>
            <td>TENET Healthcare Corporation</td>
            <td>None</td>
            <td>TN</td>
            <td>159.0</td>
        </tr>
        <tr>
            <td>TENET Healthcare Corporation</td>
            <td>None</td>
            <td>TX</td>
            <td>159.0</td>
        </tr>
        <tr>
            <td>TENET Healthcare Corporation</td>
            <td>None</td>
            <td>MI</td>
            <td>159.0</td>
        </tr>
        <tr>
            <td>TENET Healthcare Corporation</td>
            <td>None</td>
            <td>SC</td>
            <td>159.0</td>
        </tr>
        <tr>
            <td>Southside Regional Medical Center</td>
            <td>Petersburg</td>
            <td>VA</td>
            <td>160.0</td>
        </tr>
        <tr>
            <td>Deaconess Health System</td>
            <td>None</td>
            <td>IN</td>
            <td>160.0</td>
        </tr>
        <tr>
            <td>Deaconess Health System</td>
            <td>None</td>
            <td>KY</td>
            <td>160.0</td>
        </tr>
        <tr>
            <td>AllianceHealth Durant</td>
            <td>Durant</td>
            <td>OK</td>
            <td>161.0</td>
        </tr>
        <tr>
            <td>Carilion Clinic</td>
            <td>None</td>
            <td>VA</td>
            <td>161.0</td>
        </tr>
        <tr>
            <td>St. Johns Regional Medical Center</td>
            <td>Oxnard</td>
            <td>CA</td>
            <td>162.0</td>
        </tr>
        <tr>
            <td>Community Health Network</td>
            <td>None</td>
            <td>IN</td>
            <td>162.0</td>
        </tr>
        <tr>
            <td>Bertrand Chaffee Hospital</td>
            <td>Springville</td>
            <td>NY</td>
            <td>163.0</td>
        </tr>
        <tr>
            <td>Memorial Health System</td>
            <td>None</td>
            <td>IL</td>
            <td>163.0</td>
        </tr>
        <tr>
            <td>Spencer Municipal Hospital</td>
            <td>Spencer</td>
            <td>IA</td>
            <td>164.0</td>
        </tr>
        <tr>
            <td>RWJBarnabas Health</td>
            <td>None</td>
            <td>NJ</td>
            <td>164.0</td>
        </tr>
        <tr>
            <td>Integris Southwest Medical Center</td>
            <td>Oklahoma City</td>
            <td>OK</td>
            <td>165.0</td>
        </tr>
        <tr>
            <td>Cape Fear Valley Health System</td>
            <td>None</td>
            <td>NC</td>
            <td>165.0</td>
        </tr>
        <tr>
            <td>Ascension Our Lady of Victory Hospital</td>
            <td>Stanley</td>
            <td>WI</td>
            <td>166.0</td>
        </tr>
        <tr>
            <td>Sentara Healthcare</td>
            <td>None</td>
            <td>NC</td>
            <td>166.0</td>
        </tr>
        <tr>
            <td>Sentara Healthcare</td>
            <td>None</td>
            <td>VA</td>
            <td>166.0</td>
        </tr>
        <tr>
            <td>St. Francis Regional Medical Center</td>
            <td>Shakopee</td>
            <td>MN</td>
            <td>167.0</td>
        </tr>
        <tr>
            <td>Prisma Health</td>
            <td>None</td>
            <td>SC</td>
            <td>167.0</td>
        </tr>
        <tr>
            <td>Mclaren Oakland</td>
            <td>Pontiac</td>
            <td>MI</td>
            <td>168.0</td>
        </tr>
        <tr>
            <td>Willis-Knighton Health System</td>
            <td>None</td>
            <td>LA</td>
            <td>168.0</td>
        </tr>
        <tr>
            <td>St. Alexius Hospital</td>
            <td>Saint Louis</td>
            <td>MO</td>
            <td>169.0</td>
        </tr>
        <tr>
            <td>LCMC Health System</td>
            <td>None</td>
            <td>LA</td>
            <td>169.0</td>
        </tr>
        <tr>
            <td>Russell County Hospital</td>
            <td>Lebanon</td>
            <td>VA</td>
            <td>170.0</td>
        </tr>
        <tr>
            <td>Marshfield Clinic Health System</td>
            <td>None</td>
            <td>WI</td>
            <td>170.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Logan County</td>
            <td>Guthrie</td>
            <td>OK</td>
            <td>171.0</td>
        </tr>
        <tr>
            <td>Meadville Medical Center</td>
            <td>None</td>
            <td>PA</td>
            <td>171.0</td>
        </tr>
        <tr>
            <td>Palms West Hospital</td>
            <td>Loxahatchee</td>
            <td>FL</td>
            <td>172.0</td>
        </tr>
        <tr>
            <td>PIH Health</td>
            <td>None</td>
            <td>CA</td>
            <td>172.0</td>
        </tr>
        <tr>
            <td>Bayshore Medical Center</td>
            <td>Pasadena</td>
            <td>TX</td>
            <td>173.0</td>
        </tr>
        <tr>
            <td>Covenant Health</td>
            <td>None</td>
            <td>TN</td>
            <td>173.0</td>
        </tr>
        <tr>
            <td>Community Hospital</td>
            <td>Tallassee</td>
            <td>AL</td>
            <td>174.0</td>
        </tr>
        <tr>
            <td>Parkview Health System</td>
            <td>None</td>
            <td>IN</td>
            <td>174.0</td>
        </tr>
        <tr>
            <td>University of Maryland Medical Center</td>
            <td>Baltimore</td>
            <td>MD</td>
            <td>175.0</td>
        </tr>
        <tr>
            <td>Kaleida Health</td>
            <td>None</td>
            <td>NY</td>
            <td>175.0</td>
        </tr>
        <tr>
            <td>Johns Hopkins Bayview Medical Center</td>
            <td>Baltimore</td>
            <td>MD</td>
            <td>176.0</td>
        </tr>
        <tr>
            <td>Penn State Health</td>
            <td>None</td>
            <td>PA</td>
            <td>176.0</td>
        </tr>
        <tr>
            <td>Harrison Memorial Hospital</td>
            <td>Cynthiana</td>
            <td>KY</td>
            <td>177.0</td>
        </tr>
        <tr>
            <td>Health Quest Systems</td>
            <td>None</td>
            <td>CT</td>
            <td>177.0</td>
        </tr>
        <tr>
            <td>Health Quest Systems</td>
            <td>None</td>
            <td>NY</td>
            <td>177.0</td>
        </tr>
        <tr>
            <td>Jewish Hospital - Shelbyville</td>
            <td>Shelbyville</td>
            <td>KY</td>
            <td>178.0</td>
        </tr>
        <tr>
            <td>Hartford Healthcare</td>
            <td>None</td>
            <td>CT</td>
            <td>178.0</td>
        </tr>
        <tr>
            <td>Adventist Health Portland</td>
            <td>Portland</td>
            <td>OR</td>
            <td>179.0</td>
        </tr>
        <tr>
            <td>Blessing Health System</td>
            <td>None</td>
            <td>IL</td>
            <td>179.0</td>
        </tr>
        <tr>
            <td>Blessing Health System</td>
            <td>None</td>
            <td>IA</td>
            <td>179.0</td>
        </tr>
        <tr>
            <td>Montefiore Medical Center</td>
            <td>Bronx</td>
            <td>NY</td>
            <td>180.0</td>
        </tr>
        <tr>
            <td>Franciscan Missionaries of Our Lady Health System</td>
            <td>None</td>
            <td>LA</td>
            <td>180.0</td>
        </tr>
        <tr>
            <td>Banner Payson Medical Center</td>
            <td>Payson</td>
            <td>AZ</td>
            <td>181.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Health System</td>
            <td>None</td>
            <td>ID</td>
            <td>181.0</td>
        </tr>
        <tr>
            <td>Palm Bay Hospital</td>
            <td>Palm Bay</td>
            <td>FL</td>
            <td>182.0</td>
        </tr>
        <tr>
            <td>Hospital Sisters Health System</td>
            <td>None</td>
            <td>IL</td>
            <td>182.0</td>
        </tr>
        <tr>
            <td>Hospital Sisters Health System</td>
            <td>None</td>
            <td>WI</td>
            <td>182.0</td>
        </tr>
        <tr>
            <td>Southern Maine Health Care</td>
            <td>Biddeford</td>
            <td>ME</td>
            <td>183.0</td>
        </tr>
        <tr>
            <td>Nuvance Health</td>
            <td>None</td>
            <td>CT</td>
            <td>183.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Nampa Medical Center</td>
            <td>Nampa</td>
            <td>ID</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>KY</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>KS</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>AR</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>WA</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>CA</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>AZ</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>IA</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>CO</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>GA</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>OR</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>OH</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>TX</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>TN</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>NE</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>MN</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>ND</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>CommonSpirit Health</td>
            <td>None</td>
            <td>NV</td>
            <td>184.0</td>
        </tr>
        <tr>
            <td>Valley Hospital Medical Center</td>
            <td>Las Vegas</td>
            <td>NV</td>
            <td>185.0</td>
        </tr>
        <tr>
            <td>Penn Highlands Healthcare</td>
            <td>None</td>
            <td>PA</td>
            <td>185.0</td>
        </tr>
        <tr>
            <td>Methodist Hospitals</td>
            <td>Gary</td>
            <td>IN</td>
            <td>186.0</td>
        </tr>
        <tr>
            <td>LifeBridge Health</td>
            <td>None</td>
            <td>MD</td>
            <td>186.0</td>
        </tr>
        <tr>
            <td>St. Vincent&#x27;s Chilton</td>
            <td>Clanton</td>
            <td>AL</td>
            <td>187.0</td>
        </tr>
        <tr>
            <td>Queen&#x27;s Health Systems</td>
            <td>None</td>
            <td>HI</td>
            <td>187.0</td>
        </tr>
        <tr>
            <td>Baylor Scott &amp; White Medical Center - Taylor</td>
            <td>Taylor</td>
            <td>TX</td>
            <td>188.0</td>
        </tr>
        <tr>
            <td>Legacy Health</td>
            <td>None</td>
            <td>OR</td>
            <td>188.0</td>
        </tr>
        <tr>
            <td>Legacy Health</td>
            <td>None</td>
            <td>WA</td>
            <td>188.0</td>
        </tr>
        <tr>
            <td>Hemet Valley Medical Center</td>
            <td>Hemet</td>
            <td>CA</td>
            <td>189.0</td>
        </tr>
        <tr>
            <td>Cayuga Medical Center</td>
            <td>None</td>
            <td>NY</td>
            <td>189.0</td>
        </tr>
        <tr>
            <td>Nathan Littauer Hospital</td>
            <td>Gloversville</td>
            <td>NY</td>
            <td>190.0</td>
        </tr>
        <tr>
            <td>McLaren Health Care Corporation</td>
            <td>None</td>
            <td>MI</td>
            <td>190.0</td>
        </tr>
        <tr>
            <td>Holy Cross Germantown Hospital</td>
            <td>Germantown</td>
            <td>MD</td>
            <td>191.0</td>
        </tr>
        <tr>
            <td>Memorial Hermann Health System</td>
            <td>None</td>
            <td>TX</td>
            <td>191.0</td>
        </tr>
        <tr>
            <td>Sunrise Hospital and Medical Center</td>
            <td>Las Vegas</td>
            <td>NV</td>
            <td>192.0</td>
        </tr>
        <tr>
            <td>Orlando Health</td>
            <td>None</td>
            <td>FL</td>
            <td>192.0</td>
        </tr>
        <tr>
            <td>Good Shepherd Medical Center</td>
            <td>Hermiston</td>
            <td>OR</td>
            <td>193.0</td>
        </tr>
        <tr>
            <td>Duke University Health System</td>
            <td>None</td>
            <td>NC</td>
            <td>193.0</td>
        </tr>
        <tr>
            <td>Oakbend Medical Center</td>
            <td>Richmond</td>
            <td>TX</td>
            <td>194.0</td>
        </tr>
        <tr>
            <td>Stillwater Medical Center Authority</td>
            <td>None</td>
            <td>OK</td>
            <td>194.0</td>
        </tr>
        <tr>
            <td>Centinela Hospital Medical Center</td>
            <td>Inglewood</td>
            <td>CA</td>
            <td>195.0</td>
        </tr>
        <tr>
            <td>North Country Healthcare</td>
            <td>None</td>
            <td>NH</td>
            <td>195.0</td>
        </tr>
        <tr>
            <td>Colorado River Medical Center</td>
            <td>Needles</td>
            <td>CA</td>
            <td>196.0</td>
        </tr>
        <tr>
            <td>Avera Health</td>
            <td>None</td>
            <td>MN</td>
            <td>196.0</td>
        </tr>
        <tr>
            <td>Avera Health</td>
            <td>None</td>
            <td>IA</td>
            <td>196.0</td>
        </tr>
        <tr>
            <td>Avera Health</td>
            <td>None</td>
            <td>SD</td>
            <td>196.0</td>
        </tr>
        <tr>
            <td>Avera Health</td>
            <td>None</td>
            <td>NE</td>
            <td>196.0</td>
        </tr>
        <tr>
            <td>Sentara Albemarle Medical Center</td>
            <td>Elizabeth City</td>
            <td>NC</td>
            <td>197.0</td>
        </tr>
        <tr>
            <td>Lifespan</td>
            <td>None</td>
            <td>RI</td>
            <td>197.0</td>
        </tr>
        <tr>
            <td>Scotland County  Hospital</td>
            <td>Memphis</td>
            <td>MO</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>IA</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>IL</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>DE</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>NY</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>CT</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>CA</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>GA</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>FL</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>OH</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>MI</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>PA</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>OR</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>IN</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>ID</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>MA</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Trinity Health</td>
            <td>None</td>
            <td>MD</td>
            <td>198.0</td>
        </tr>
        <tr>
            <td>Moberly Regional Medical Center</td>
            <td>Moberly</td>
            <td>MO</td>
            <td>199.0</td>
        </tr>
        <tr>
            <td>Baptist Memorial Health Care Corporation</td>
            <td>None</td>
            <td>AR</td>
            <td>199.0</td>
        </tr>
        <tr>
            <td>Baptist Memorial Health Care Corporation</td>
            <td>None</td>
            <td>MS</td>
            <td>199.0</td>
        </tr>
        <tr>
            <td>Baptist Memorial Health Care Corporation</td>
            <td>None</td>
            <td>TN</td>
            <td>199.0</td>
        </tr>
        <tr>
            <td>Palmdale Regional Medical Center</td>
            <td>Palmdale</td>
            <td>CA</td>
            <td>200.0</td>
        </tr>
        <tr>
            <td>UPMC</td>
            <td>None</td>
            <td>MD</td>
            <td>200.0</td>
        </tr>
        <tr>
            <td>UPMC</td>
            <td>None</td>
            <td>NY</td>
            <td>200.0</td>
        </tr>
        <tr>
            <td>UPMC</td>
            <td>None</td>
            <td>PA</td>
            <td>200.0</td>
        </tr>
        <tr>
            <td>Research Medical Center</td>
            <td>Kansas City</td>
            <td>MO</td>
            <td>201.0</td>
        </tr>
        <tr>
            <td>UNC Health</td>
            <td>None</td>
            <td>NC</td>
            <td>201.0</td>
        </tr>
        <tr>
            <td>Sutter Delta Medical Center</td>
            <td>Antioch</td>
            <td>CA</td>
            <td>202.0</td>
        </tr>
        <tr>
            <td>Nebraska Methodist Health System</td>
            <td>None</td>
            <td>IA</td>
            <td>202.0</td>
        </tr>
        <tr>
            <td>Nebraska Methodist Health System</td>
            <td>None</td>
            <td>NE</td>
            <td>202.0</td>
        </tr>
        <tr>
            <td>Benefis Hospitals</td>
            <td>Great Falls</td>
            <td>MT</td>
            <td>203.0</td>
        </tr>
        <tr>
            <td>OhioHealth</td>
            <td>None</td>
            <td>OH</td>
            <td>203.0</td>
        </tr>
        <tr>
            <td>Eskenazi Health</td>
            <td>Indianapolis</td>
            <td>IN</td>
            <td>204.0</td>
        </tr>
        <tr>
            <td>Asante Health System</td>
            <td>None</td>
            <td>OR</td>
            <td>204.0</td>
        </tr>
        <tr>
            <td>Sycamore Shoals Hospital</td>
            <td>Elizabethton</td>
            <td>TN</td>
            <td>205.0</td>
        </tr>
        <tr>
            <td>Phoebe Putney Health Systems</td>
            <td>None</td>
            <td>GA</td>
            <td>205.0</td>
        </tr>
        <tr>
            <td>Methodist Hospital South</td>
            <td>Jourdanton</td>
            <td>TX</td>
            <td>206.0</td>
        </tr>
        <tr>
            <td>Bryan Health</td>
            <td>None</td>
            <td>NE</td>
            <td>206.0</td>
        </tr>
        <tr>
            <td>Highland Hospital</td>
            <td>Oakland</td>
            <td>CA</td>
            <td>207.0</td>
        </tr>
        <tr>
            <td>White River Health System</td>
            <td>None</td>
            <td>AR</td>
            <td>207.0</td>
        </tr>
        <tr>
            <td>Phoenixville Hospital</td>
            <td>Phoenixville</td>
            <td>PA</td>
            <td>208.0</td>
        </tr>
        <tr>
            <td>Novant Health</td>
            <td>None</td>
            <td>NC</td>
            <td>208.0</td>
        </tr>
        <tr>
            <td>Palmetto General Hospital</td>
            <td>Hialeah</td>
            <td>FL</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>GA</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>FL</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>MS</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>IN</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>AK</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>AL</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>AR</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>AZ</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>TN</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>PA</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>WV</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>TX</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>NM</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>MO</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>OK</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Community Health Systems</td>
            <td>None</td>
            <td>NC</td>
            <td>209.0</td>
        </tr>
        <tr>
            <td>Carilion Giles Community Hospital</td>
            <td>Pearisburg</td>
            <td>VA</td>
            <td>210.0</td>
        </tr>
        <tr>
            <td>Baptist Health Care</td>
            <td>None</td>
            <td>FL</td>
            <td>210.0</td>
        </tr>
        <tr>
            <td>Ephraim Mcdowell Regional Medical Center</td>
            <td>Danville</td>
            <td>KY</td>
            <td>211.0</td>
        </tr>
        <tr>
            <td>CHRISTUS Health</td>
            <td>None</td>
            <td>LA</td>
            <td>211.0</td>
        </tr>
        <tr>
            <td>CHRISTUS Health</td>
            <td>None</td>
            <td>NM</td>
            <td>211.0</td>
        </tr>
        <tr>
            <td>CHRISTUS Health</td>
            <td>None</td>
            <td>TX</td>
            <td>211.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System-Chippewa Valley</td>
            <td>Bloomer</td>
            <td>WI</td>
            <td>212.0</td>
        </tr>
        <tr>
            <td>Tift Regional Health System</td>
            <td>None</td>
            <td>GA</td>
            <td>212.0</td>
        </tr>
        <tr>
            <td>Elkview General Hospital</td>
            <td>Hobart</td>
            <td>OK</td>
            <td>213.0</td>
        </tr>
        <tr>
            <td>Community Hospital Corporation</td>
            <td>None</td>
            <td>TX</td>
            <td>213.0</td>
        </tr>
        <tr>
            <td>Community Hospital Corporation</td>
            <td>None</td>
            <td>NM</td>
            <td>213.0</td>
        </tr>
        <tr>
            <td>Kauai Veterans Memorial Hospital</td>
            <td>Waimea</td>
            <td>HI</td>
            <td>214.0</td>
        </tr>
        <tr>
            <td>M Health Fairview</td>
            <td>None</td>
            <td>MN</td>
            <td>214.0</td>
        </tr>
        <tr>
            <td>ACMH Hospital</td>
            <td>Kittanning</td>
            <td>PA</td>
            <td>215.0</td>
        </tr>
        <tr>
            <td>Vanderbilt Health</td>
            <td>None</td>
            <td>TN</td>
            <td>215.0</td>
        </tr>
        <tr>
            <td>Roane Medical Center</td>
            <td>Harriman</td>
            <td>TN</td>
            <td>216.0</td>
        </tr>
        <tr>
            <td>Concord Hospital Health System</td>
            <td>None</td>
            <td>NH</td>
            <td>216.0</td>
        </tr>
        <tr>
            <td>Southern California Hospital at Hollywood</td>
            <td>Hollywood</td>
            <td>CA</td>
            <td>217.0</td>
        </tr>
        <tr>
            <td>Emanate Health</td>
            <td>None</td>
            <td>CA</td>
            <td>217.0</td>
        </tr>
        <tr>
            <td>West Jefferson Medical Center</td>
            <td>Marrero</td>
            <td>LA</td>
            <td>218.0</td>
        </tr>
        <tr>
            <td>Covenant Health Systems</td>
            <td>None</td>
            <td>ME</td>
            <td>218.0</td>
        </tr>
        <tr>
            <td>Covenant Health Systems</td>
            <td>None</td>
            <td>NH</td>
            <td>218.0</td>
        </tr>
        <tr>
            <td>Jefferson Regional Medical Center</td>
            <td>Pine Bluff</td>
            <td>AR</td>
            <td>219.0</td>
        </tr>
        <tr>
            <td>Faith Regional Health Services</td>
            <td>None</td>
            <td>NE</td>
            <td>219.0</td>
        </tr>
        <tr>
            <td>Antelope Valley Hospital</td>
            <td>Lancaster</td>
            <td>CA</td>
            <td>220.0</td>
        </tr>
        <tr>
            <td>University of Rochester Medical Center</td>
            <td>None</td>
            <td>NY</td>
            <td>220.0</td>
        </tr>
        <tr>
            <td>Holy Cross Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>221.0</td>
        </tr>
        <tr>
            <td>Cone Health</td>
            <td>None</td>
            <td>NC</td>
            <td>221.0</td>
        </tr>
        <tr>
            <td>Westfields Hospital and Clinic</td>
            <td>New Richmond</td>
            <td>WI</td>
            <td>222.0</td>
        </tr>
        <tr>
            <td>Advocate Aurora Health</td>
            <td>None</td>
            <td>IL</td>
            <td>222.0</td>
        </tr>
        <tr>
            <td>Advocate Aurora Health</td>
            <td>None</td>
            <td>WI</td>
            <td>222.0</td>
        </tr>
        <tr>
            <td>St. Joseph&#x27;s University Medical Center</td>
            <td>Paterson</td>
            <td>NJ</td>
            <td>223.0</td>
        </tr>
        <tr>
            <td>Froedtert and The Medical College of Wisconsin</td>
            <td>None</td>
            <td>WI</td>
            <td>223.0</td>
        </tr>
        <tr>
            <td>Flushing Hospital Medical Center</td>
            <td>Flushing</td>
            <td>NY</td>
            <td>224.0</td>
        </tr>
        <tr>
            <td>BJC Healthcare</td>
            <td>None</td>
            <td>IL</td>
            <td>224.0</td>
        </tr>
        <tr>
            <td>BJC Healthcare</td>
            <td>None</td>
            <td>MO</td>
            <td>224.0</td>
        </tr>
        <tr>
            <td>Medstar Union Memorial Hospital</td>
            <td>Baltimore</td>
            <td>MD</td>
            <td>225.0</td>
        </tr>
        <tr>
            <td>HealthPartners</td>
            <td>None</td>
            <td>MN</td>
            <td>225.0</td>
        </tr>
        <tr>
            <td>HealthPartners</td>
            <td>None</td>
            <td>WI</td>
            <td>225.0</td>
        </tr>
        <tr>
            <td>Holy Cross Hospital</td>
            <td>Silver Spring</td>
            <td>MD</td>
            <td>226.0</td>
        </tr>
        <tr>
            <td>Baptist Health</td>
            <td>None</td>
            <td>IN</td>
            <td>226.0</td>
        </tr>
        <tr>
            <td>Baptist Health</td>
            <td>None</td>
            <td>KY</td>
            <td>226.0</td>
        </tr>
        <tr>
            <td>St. Vincent&#x27;s Medical Center Riverside</td>
            <td>Jacksonville</td>
            <td>FL</td>
            <td>227.0</td>
        </tr>
        <tr>
            <td>Bassett Healthcare Network</td>
            <td>None</td>
            <td>NY</td>
            <td>227.0</td>
        </tr>
        <tr>
            <td>Spotsylvania Regional Medical Center</td>
            <td>Fredericksburg</td>
            <td>VA</td>
            <td>228.0</td>
        </tr>
        <tr>
            <td>Mountain Health Network</td>
            <td>None</td>
            <td>WV</td>
            <td>228.0</td>
        </tr>
        <tr>
            <td>North Okaloosa Medical Center</td>
            <td>Crestview</td>
            <td>FL</td>
            <td>229.0</td>
        </tr>
        <tr>
            <td>Firsthealth of The Carolinas</td>
            <td>None</td>
            <td>NC</td>
            <td>229.0</td>
        </tr>
        <tr>
            <td>Penn Presbyterian Medical Center</td>
            <td>Philadelphia</td>
            <td>PA</td>
            <td>230.0</td>
        </tr>
        <tr>
            <td>Piedmont Healthcare</td>
            <td>None</td>
            <td>GA</td>
            <td>230.0</td>
        </tr>
        <tr>
            <td>California Pacific Medical Center- Van Ness Campus</td>
            <td>San Francisco</td>
            <td>CA</td>
            <td>231.0</td>
        </tr>
        <tr>
            <td>Ardent Health Services</td>
            <td>None</td>
            <td>NJ</td>
            <td>231.0</td>
        </tr>
        <tr>
            <td>Ardent Health Services</td>
            <td>None</td>
            <td>ID</td>
            <td>231.0</td>
        </tr>
        <tr>
            <td>Ardent Health Services</td>
            <td>None</td>
            <td>NM</td>
            <td>231.0</td>
        </tr>
        <tr>
            <td>Ardent Health Services</td>
            <td>None</td>
            <td>TX</td>
            <td>231.0</td>
        </tr>
        <tr>
            <td>Ardent Health Services</td>
            <td>None</td>
            <td>OK</td>
            <td>231.0</td>
        </tr>
        <tr>
            <td>Regional One Health</td>
            <td>Memphis</td>
            <td>TN</td>
            <td>232.0</td>
        </tr>
        <tr>
            <td>Munson Healthcare</td>
            <td>None</td>
            <td>MI</td>
            <td>232.0</td>
        </tr>
        <tr>
            <td>Baylor Scott and White Medical Center Carrollton</td>
            <td>Carrollton</td>
            <td>TX</td>
            <td>233.0</td>
        </tr>
        <tr>
            <td>St. Lawrence Health System</td>
            <td>None</td>
            <td>NY</td>
            <td>233.0</td>
        </tr>
        <tr>
            <td>Grady Memorial Hospital</td>
            <td>Delaware</td>
            <td>OH</td>
            <td>234.0</td>
        </tr>
        <tr>
            <td>Baptist Health</td>
            <td>None</td>
            <td>AL</td>
            <td>234.0</td>
        </tr>
        <tr>
            <td>University Medical Center New Orleans</td>
            <td>New Orleans</td>
            <td>LA</td>
            <td>235.0</td>
        </tr>
        <tr>
            <td>Northeast Georgia Health System</td>
            <td>None</td>
            <td>GA</td>
            <td>235.0</td>
        </tr>
        <tr>
            <td>Doctors Hospital</td>
            <td>Columbus</td>
            <td>OH</td>
            <td>236.0</td>
        </tr>
        <tr>
            <td>Christiana Care Health System</td>
            <td>None</td>
            <td>DE</td>
            <td>236.0</td>
        </tr>
        <tr>
            <td>Christiana Care Health System</td>
            <td>None</td>
            <td>MD</td>
            <td>236.0</td>
        </tr>
        <tr>
            <td>Watsonville Community Hospital</td>
            <td>Watsonville</td>
            <td>CA</td>
            <td>237.0</td>
        </tr>
        <tr>
            <td>Yale New Haven Health System</td>
            <td>None</td>
            <td>CT</td>
            <td>237.0</td>
        </tr>
        <tr>
            <td>Yale New Haven Health System</td>
            <td>None</td>
            <td>RI</td>
            <td>237.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Clermont</td>
            <td>Batavia</td>
            <td>OH</td>
            <td>238.0</td>
        </tr>
        <tr>
            <td>University of Texas Health System</td>
            <td>None</td>
            <td>TX</td>
            <td>238.0</td>
        </tr>
        <tr>
            <td>Zuckerberg San Francisco General Hosp &amp; Trauma Center</td>
            <td>San Francisco</td>
            <td>CA</td>
            <td>239.0</td>
        </tr>
        <tr>
            <td>Saint Bernards Healthcare</td>
            <td>None</td>
            <td>AR</td>
            <td>239.0</td>
        </tr>
        <tr>
            <td>St. Charles Prineville</td>
            <td>Prineville</td>
            <td>OR</td>
            <td>240.0</td>
        </tr>
        <tr>
            <td>AdventHealth</td>
            <td>None</td>
            <td>GA</td>
            <td>240.0</td>
        </tr>
        <tr>
            <td>AdventHealth</td>
            <td>None</td>
            <td>IL</td>
            <td>240.0</td>
        </tr>
        <tr>
            <td>AdventHealth</td>
            <td>None</td>
            <td>CO</td>
            <td>240.0</td>
        </tr>
        <tr>
            <td>AdventHealth</td>
            <td>None</td>
            <td>FL</td>
            <td>240.0</td>
        </tr>
        <tr>
            <td>AdventHealth</td>
            <td>None</td>
            <td>KS</td>
            <td>240.0</td>
        </tr>
        <tr>
            <td>AdventHealth</td>
            <td>None</td>
            <td>TX</td>
            <td>240.0</td>
        </tr>
        <tr>
            <td>AdventHealth</td>
            <td>None</td>
            <td>WI</td>
            <td>240.0</td>
        </tr>
        <tr>
            <td>AdventHealth</td>
            <td>None</td>
            <td>KY</td>
            <td>240.0</td>
        </tr>
        <tr>
            <td>AdventHealth</td>
            <td>None</td>
            <td>NC</td>
            <td>240.0</td>
        </tr>
        <tr>
            <td>Eastern Maine Medical Center</td>
            <td>Bangor</td>
            <td>ME</td>
            <td>241.0</td>
        </tr>
        <tr>
            <td>MercyOne</td>
            <td>None</td>
            <td>IA</td>
            <td>241.0</td>
        </tr>
        <tr>
            <td>Watertown Regional Medical Center</td>
            <td>Watertown</td>
            <td>WI</td>
            <td>242.0</td>
        </tr>
        <tr>
            <td>Tidelands Health</td>
            <td>None</td>
            <td>SC</td>
            <td>242.0</td>
        </tr>
        <tr>
            <td>Candler Hospital</td>
            <td>Savannah</td>
            <td>GA</td>
            <td>243.0</td>
        </tr>
        <tr>
            <td>Texas Health Resources</td>
            <td>None</td>
            <td>TX</td>
            <td>243.0</td>
        </tr>
        <tr>
            <td>Duke Regional Hospital</td>
            <td>Durham</td>
            <td>NC</td>
            <td>244.0</td>
        </tr>
        <tr>
            <td>Hackensack Meridian Health</td>
            <td>None</td>
            <td>NJ</td>
            <td>244.0</td>
        </tr>
        <tr>
            <td>Adventist Health Bakersfield</td>
            <td>Bakersfield</td>
            <td>CA</td>
            <td>245.0</td>
        </tr>
        <tr>
            <td>Mercy</td>
            <td>None</td>
            <td>AR</td>
            <td>245.0</td>
        </tr>
        <tr>
            <td>Mercy</td>
            <td>None</td>
            <td>MO</td>
            <td>245.0</td>
        </tr>
        <tr>
            <td>Mercy</td>
            <td>None</td>
            <td>OK</td>
            <td>245.0</td>
        </tr>
        <tr>
            <td>Desoto Regional Health System</td>
            <td>Mansfield</td>
            <td>LA</td>
            <td>246.0</td>
        </tr>
        <tr>
            <td>MaineHealth</td>
            <td>None</td>
            <td>ME</td>
            <td>246.0</td>
        </tr>
        <tr>
            <td>MaineHealth</td>
            <td>None</td>
            <td>NH</td>
            <td>246.0</td>
        </tr>
        <tr>
            <td>Harris Regional Hospital</td>
            <td>Sylva</td>
            <td>NC</td>
            <td>247.0</td>
        </tr>
        <tr>
            <td>University Hospitals</td>
            <td>None</td>
            <td>OH</td>
            <td>247.0</td>
        </tr>
        <tr>
            <td>Union County General Hospital</td>
            <td>Clayton</td>
            <td>NM</td>
            <td>248.0</td>
        </tr>
        <tr>
            <td>Hawaii Pacific Health</td>
            <td>None</td>
            <td>HI</td>
            <td>248.0</td>
        </tr>
        <tr>
            <td>Coral Gables Hospital</td>
            <td>Coral Gables</td>
            <td>FL</td>
            <td>249.0</td>
        </tr>
        <tr>
            <td>Kettering Health Network</td>
            <td>None</td>
            <td>OH</td>
            <td>249.0</td>
        </tr>
        <tr>
            <td>St. Lucie Medical Center</td>
            <td>Port Saint Lucie</td>
            <td>FL</td>
            <td>250.0</td>
        </tr>
        <tr>
            <td>Carle Health</td>
            <td>None</td>
            <td>IL</td>
            <td>250.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System-Oakridge</td>
            <td>Osseo</td>
            <td>WI</td>
            <td>251.0</td>
        </tr>
        <tr>
            <td>Baptist Health</td>
            <td>None</td>
            <td>FL</td>
            <td>251.0</td>
        </tr>
        <tr>
            <td>Tristar Stonecrest Medical Center</td>
            <td>Smyrna</td>
            <td>TN</td>
            <td>252.0</td>
        </tr>
        <tr>
            <td>Saint Luke&#x27;s Health System</td>
            <td>None</td>
            <td>KS</td>
            <td>252.0</td>
        </tr>
        <tr>
            <td>Saint Luke&#x27;s Health System</td>
            <td>None</td>
            <td>MO</td>
            <td>252.0</td>
        </tr>
        <tr>
            <td>St. Vincent&#x27;s St. Clair</td>
            <td>Pell City</td>
            <td>AL</td>
            <td>253.0</td>
        </tr>
        <tr>
            <td>MemorialCare</td>
            <td>None</td>
            <td>CA</td>
            <td>253.0</td>
        </tr>
        <tr>
            <td>Medical West, An Affiliate of UAB Health System</td>
            <td>Bessemer</td>
            <td>AL</td>
            <td>254.0</td>
        </tr>
        <tr>
            <td>Mon Health</td>
            <td>None</td>
            <td>WV</td>
            <td>254.0</td>
        </tr>
        <tr>
            <td>Milan General Hospital</td>
            <td>Milan</td>
            <td>TN</td>
            <td>255.0</td>
        </tr>
        <tr>
            <td>Emory Healthcare</td>
            <td>None</td>
            <td>GA</td>
            <td>255.0</td>
        </tr>
        <tr>
            <td>Clifton Springs Hospital and Clinic</td>
            <td>Clifton Springs</td>
            <td>NY</td>
            <td>256.0</td>
        </tr>
        <tr>
            <td>University of Maryland Medical System</td>
            <td>None</td>
            <td>MD</td>
            <td>256.0</td>
        </tr>
        <tr>
            <td>Spectrum Health United Hospital</td>
            <td>Greenville</td>
            <td>MI</td>
            <td>257.0</td>
        </tr>
        <tr>
            <td>Houston Healthcare</td>
            <td>None</td>
            <td>GA</td>
            <td>257.0</td>
        </tr>
        <tr>
            <td>Cheyenne Regional Medical Center</td>
            <td>Cheyenne</td>
            <td>WY</td>
            <td>258.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic</td>
            <td>None</td>
            <td>FL</td>
            <td>258.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic</td>
            <td>None</td>
            <td>AZ</td>
            <td>258.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic</td>
            <td>None</td>
            <td>IA</td>
            <td>258.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic</td>
            <td>None</td>
            <td>WI</td>
            <td>258.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic</td>
            <td>None</td>
            <td>MN</td>
            <td>258.0</td>
        </tr>
        <tr>
            <td>Saint Joseph Berea</td>
            <td>Berea</td>
            <td>KY</td>
            <td>259.0</td>
        </tr>
        <tr>
            <td>Olathe Health System</td>
            <td>None</td>
            <td>KS</td>
            <td>259.0</td>
        </tr>
        <tr>
            <td>Healthmark Regional Medical Center</td>
            <td>Defuniak Springs</td>
            <td>FL</td>
            <td>260.0</td>
        </tr>
        <tr>
            <td>Northside Healthcare System</td>
            <td>None</td>
            <td>GA</td>
            <td>260.0</td>
        </tr>
        <tr>
            <td>Sentara Northern Virginia Medical Center</td>
            <td>Woodbridge</td>
            <td>VA</td>
            <td>261.0</td>
        </tr>
        <tr>
            <td>Renown Health</td>
            <td>None</td>
            <td>NV</td>
            <td>261.0</td>
        </tr>
        <tr>
            <td>Thorek Memorial Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>262.0</td>
        </tr>
        <tr>
            <td>Riverside Health System</td>
            <td>None</td>
            <td>VA</td>
            <td>262.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Lincoln</td>
            <td>Troy</td>
            <td>MO</td>
            <td>263.0</td>
        </tr>
        <tr>
            <td>University of Pennsylvania Health System</td>
            <td>None</td>
            <td>PA</td>
            <td>263.0</td>
        </tr>
        <tr>
            <td>University of Pennsylvania Health System</td>
            <td>None</td>
            <td>NJ</td>
            <td>263.0</td>
        </tr>
        <tr>
            <td>Robert Packer Hospital</td>
            <td>Sayre</td>
            <td>PA</td>
            <td>264.0</td>
        </tr>
        <tr>
            <td>Montefiore Medical Center</td>
            <td>None</td>
            <td>NY</td>
            <td>264.0</td>
        </tr>
        <tr>
            <td>Excela Health Frick Hospital</td>
            <td>Mount Pleasant</td>
            <td>PA</td>
            <td>265.0</td>
        </tr>
        <tr>
            <td>Mass General Brigham</td>
            <td>None</td>
            <td>MA</td>
            <td>265.0</td>
        </tr>
        <tr>
            <td>Mass General Brigham</td>
            <td>None</td>
            <td>NH</td>
            <td>265.0</td>
        </tr>
        <tr>
            <td>Citrus Memorial Hospital</td>
            <td>Inverness</td>
            <td>FL</td>
            <td>266.0</td>
        </tr>
        <tr>
            <td>Franciscan Health</td>
            <td>None</td>
            <td>IL</td>
            <td>266.0</td>
        </tr>
        <tr>
            <td>Franciscan Health</td>
            <td>None</td>
            <td>IN</td>
            <td>266.0</td>
        </tr>
        <tr>
            <td>University Medical Center</td>
            <td>Las Vegas</td>
            <td>NV</td>
            <td>267.0</td>
        </tr>
        <tr>
            <td>UW Health (Wisconsin)</td>
            <td>None</td>
            <td>IL</td>
            <td>267.0</td>
        </tr>
        <tr>
            <td>UW Health (Wisconsin)</td>
            <td>None</td>
            <td>WI</td>
            <td>267.0</td>
        </tr>
        <tr>
            <td>AdventHealth Gordon</td>
            <td>Calhoun</td>
            <td>GA</td>
            <td>268.0</td>
        </tr>
        <tr>
            <td>Broward Health</td>
            <td>None</td>
            <td>FL</td>
            <td>268.0</td>
        </tr>
        <tr>
            <td>Purcell Municipal Hospital</td>
            <td>Purcell</td>
            <td>OK</td>
            <td>269.0</td>
        </tr>
        <tr>
            <td>Jefferson Health</td>
            <td>None</td>
            <td>NJ</td>
            <td>269.0</td>
        </tr>
        <tr>
            <td>Jefferson Health</td>
            <td>None</td>
            <td>PA</td>
            <td>269.0</td>
        </tr>
        <tr>
            <td>VCU Medical Center</td>
            <td>Richmond</td>
            <td>VA</td>
            <td>270.0</td>
        </tr>
        <tr>
            <td>Intermountain Healthcare</td>
            <td>None</td>
            <td>ID</td>
            <td>270.0</td>
        </tr>
        <tr>
            <td>Intermountain Healthcare</td>
            <td>None</td>
            <td>UT</td>
            <td>270.0</td>
        </tr>
        <tr>
            <td>Dallas Regional Medical Center</td>
            <td>Mesquite</td>
            <td>TX</td>
            <td>271.0</td>
        </tr>
        <tr>
            <td>Memorial Healthcare System</td>
            <td>None</td>
            <td>FL</td>
            <td>271.0</td>
        </tr>
        <tr>
            <td>St. Mary&#x27;s Hospital</td>
            <td>Tucson</td>
            <td>AZ</td>
            <td>272.0</td>
        </tr>
        <tr>
            <td>Inova Health System</td>
            <td>None</td>
            <td>VA</td>
            <td>272.0</td>
        </tr>
        <tr>
            <td>Athens Limestone Hospital</td>
            <td>Athens</td>
            <td>AL</td>
            <td>273.0</td>
        </tr>
        <tr>
            <td>Johns Hopkins Health System</td>
            <td>None</td>
            <td>DC</td>
            <td>273.0</td>
        </tr>
        <tr>
            <td>Johns Hopkins Health System</td>
            <td>None</td>
            <td>MD</td>
            <td>273.0</td>
        </tr>
        <tr>
            <td>Saint Francis Medical Center</td>
            <td>Lynwood</td>
            <td>CA</td>
            <td>274.0</td>
        </tr>
        <tr>
            <td>Cleveland Clinic Health System</td>
            <td>None</td>
            <td>FL</td>
            <td>274.0</td>
        </tr>
        <tr>
            <td>Cleveland Clinic Health System</td>
            <td>None</td>
            <td>OH</td>
            <td>274.0</td>
        </tr>
        <tr>
            <td>Copley Memorial Hospital</td>
            <td>Aurora</td>
            <td>IL</td>
            <td>275.0</td>
        </tr>
        <tr>
            <td>Edward Elmhurst Healthcare</td>
            <td>None</td>
            <td>IL</td>
            <td>275.0</td>
        </tr>
        <tr>
            <td>Baylor Medical Center at Irving</td>
            <td>Irving</td>
            <td>TX</td>
            <td>276.0</td>
        </tr>
        <tr>
            <td>Providence</td>
            <td>None</td>
            <td>MT</td>
            <td>276.0</td>
        </tr>
        <tr>
            <td>Providence</td>
            <td>None</td>
            <td>CA</td>
            <td>276.0</td>
        </tr>
        <tr>
            <td>Providence</td>
            <td>None</td>
            <td>AK</td>
            <td>276.0</td>
        </tr>
        <tr>
            <td>Providence</td>
            <td>None</td>
            <td>WA</td>
            <td>276.0</td>
        </tr>
        <tr>
            <td>Providence</td>
            <td>None</td>
            <td>TX</td>
            <td>276.0</td>
        </tr>
        <tr>
            <td>Providence</td>
            <td>None</td>
            <td>OR</td>
            <td>276.0</td>
        </tr>
        <tr>
            <td>Sumner Regional Medical Center</td>
            <td>Gallatin</td>
            <td>TN</td>
            <td>277.0</td>
        </tr>
        <tr>
            <td>St. Elizabeth Healthcare</td>
            <td>None</td>
            <td>IN</td>
            <td>277.0</td>
        </tr>
        <tr>
            <td>St. Elizabeth Healthcare</td>
            <td>None</td>
            <td>KY</td>
            <td>277.0</td>
        </tr>
        <tr>
            <td>Adventist Health Reedley</td>
            <td>Reedley</td>
            <td>CA</td>
            <td>278.0</td>
        </tr>
        <tr>
            <td>TriHealth</td>
            <td>None</td>
            <td>OH</td>
            <td>278.0</td>
        </tr>
        <tr>
            <td>Medina Regional Hospital</td>
            <td>Hondo</td>
            <td>TX</td>
            <td>279.0</td>
        </tr>
        <tr>
            <td>Beth Israel Lahey Health</td>
            <td>None</td>
            <td>MA</td>
            <td>279.0</td>
        </tr>
        <tr>
            <td>North Suburban Medical Center</td>
            <td>Thornton</td>
            <td>CO</td>
            <td>280.0</td>
        </tr>
        <tr>
            <td>Scripps Health</td>
            <td>None</td>
            <td>CA</td>
            <td>280.0</td>
        </tr>
        <tr>
            <td>Hurley Medical Center</td>
            <td>Flint</td>
            <td>MI</td>
            <td>281.0</td>
        </tr>
        <tr>
            <td>MidMichigan Health</td>
            <td>None</td>
            <td>MI</td>
            <td>281.0</td>
        </tr>
        <tr>
            <td>Passavant Area Hospital</td>
            <td>Jacksonville</td>
            <td>IL</td>
            <td>282.0</td>
        </tr>
        <tr>
            <td>University of California Health</td>
            <td>None</td>
            <td>CA</td>
            <td>282.0</td>
        </tr>
        <tr>
            <td>Oklahoma State University Medical Center</td>
            <td>Tulsa</td>
            <td>OK</td>
            <td>283.0</td>
        </tr>
        <tr>
            <td>Virtua Health</td>
            <td>None</td>
            <td>NJ</td>
            <td>283.0</td>
        </tr>
        <tr>
            <td>OhioHealth Grant Medical Center</td>
            <td>Columbus</td>
            <td>OH</td>
            <td>284.0</td>
        </tr>
        <tr>
            <td>Houston Methodist</td>
            <td>None</td>
            <td>TX</td>
            <td>284.0</td>
        </tr>
        <tr>
            <td>Samaritan Lebanon Community Hospital</td>
            <td>Lebanon</td>
            <td>OR</td>
            <td>285.0</td>
        </tr>
        <tr>
            <td>Luminis Health</td>
            <td>None</td>
            <td>MD</td>
            <td>285.0</td>
        </tr>
        <tr>
            <td>North Shore Medical Center</td>
            <td>Miami</td>
            <td>FL</td>
            <td>286.0</td>
        </tr>
        <tr>
            <td>Beaumont Health Systems</td>
            <td>None</td>
            <td>MI</td>
            <td>286.0</td>
        </tr>
        <tr>
            <td>University of Kentucky Hospital</td>
            <td>Lexington</td>
            <td>KY</td>
            <td>287.0</td>
        </tr>
        <tr>
            <td>Northwestern Memorial Medicine</td>
            <td>None</td>
            <td>IL</td>
            <td>287.0</td>
        </tr>
        <tr>
            <td>St. Joseph Hospital</td>
            <td>Fort Wayne</td>
            <td>IN</td>
            <td>288.0</td>
        </tr>
        <tr>
            <td>New York Presbyterian</td>
            <td>None</td>
            <td>NY</td>
            <td>288.0</td>
        </tr>
        <tr>
            <td>Hennepin Healthcare - HCMC</td>
            <td>Minneapolis</td>
            <td>MN</td>
            <td>289.0</td>
        </tr>
        <tr>
            <td>Appalachian Regional Healthcare System</td>
            <td>None</td>
            <td>NC</td>
            <td>289.0</td>
        </tr>
        <tr>
            <td>Hca Houston Healthcare Pearland</td>
            <td>Pearland</td>
            <td>TX</td>
            <td>290.0</td>
        </tr>
        <tr>
            <td>Mount Sinai Health System</td>
            <td>None</td>
            <td>NY</td>
            <td>290.0</td>
        </tr>
        <tr>
            <td>Chi Health Immanuel</td>
            <td>Omaha</td>
            <td>NE</td>
            <td>291.0</td>
        </tr>
        <tr>
            <td>Stanford Health Care</td>
            <td>None</td>
            <td>CA</td>
            <td>291.0</td>
        </tr>
        <tr>
            <td>St. Mary&#x27;s of Michigan Medical Center</td>
            <td>Saginaw</td>
            <td>MI</td>
            <td>292.0</td>
        </tr>
        <tr>
            <td>Baptist Health South Florida</td>
            <td>None</td>
            <td>FL</td>
            <td>292.0</td>
        </tr>
        <tr>
            <td>Swisher Memorial Hospital</td>
            <td>Tulia</td>
            <td>TX</td>
            <td>293.0</td>
        </tr>
        <tr>
            <td>Northwell Health</td>
            <td>None</td>
            <td>NY</td>
            <td>293.0</td>
        </tr>
        <tr>
            <td>KershawHealth</td>
            <td>Camden</td>
            <td>SC</td>
            <td>294.0</td>
        </tr>
        <tr>
            <td>WMCHealth</td>
            <td>None</td>
            <td>NY</td>
            <td>294.0</td>
        </tr>
        <tr>
            <td>HCA Houston Healthcare West</td>
            <td>Houston</td>
            <td>TX</td>
            <td>295.0</td>
        </tr>
        <tr>
            <td>John Muir Health</td>
            <td>None</td>
            <td>CA</td>
            <td>295.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital</td>
            <td>Marysville</td>
            <td>OH</td>
            <td>296.0</td>
        </tr>
        <tr>
            <td>ProHealth Care</td>
            <td>None</td>
            <td>WI</td>
            <td>296.0</td>
        </tr>
        <tr>
            <td>Lehigh Valley Hospital-Schuylkill S. Jackson Street</td>
            <td>Pottsville</td>
            <td>PA</td>
            <td>297.0</td>
        </tr>
        <tr>
            <td>Catholic Health Services of Long Island</td>
            <td>None</td>
            <td>NY</td>
            <td>297.0</td>
        </tr>
        <tr>
            <td>Atrium Medical Center</td>
            <td>Franklin</td>
            <td>OH</td>
            <td>298.0</td>
        </tr>
        <tr>
            <td>HonorHealth</td>
            <td>None</td>
            <td>AZ</td>
            <td>298.0</td>
        </tr>
        <tr>
            <td>Texoma Medical Center</td>
            <td>Denison</td>
            <td>TX</td>
            <td>299.0</td>
        </tr>
        <tr>
            <td>Community Healthcare System</td>
            <td>None</td>
            <td>IN</td>
            <td>299.0</td>
        </tr>
        <tr>
            <td>St. John&#x27;s Episcopal Hospital at South Shore</td>
            <td>Far Rockaway</td>
            <td>NY</td>
            <td>300.0</td>
        </tr>
        <tr>
            <td>Main Line Health</td>
            <td>None</td>
            <td>PA</td>
            <td>300.0</td>
        </tr>
        <tr>
            <td>Covenant Medical Center</td>
            <td>Saginaw</td>
            <td>MI</td>
            <td>301.0</td>
        </tr>
        <tr>
            <td>Atlantic Health System</td>
            <td>None</td>
            <td>NJ</td>
            <td>301.0</td>
        </tr>
        <tr>
            <td>St. Joseph&#x27;s Hospital - Savannah</td>
            <td>Savannah</td>
            <td>GA</td>
            <td>302.0</td>
        </tr>
        <tr>
            <td>NorthShore University Health System</td>
            <td>None</td>
            <td>IL</td>
            <td>302.0</td>
        </tr>
        <tr>
            <td>Ochsner St. Anne General Hospital</td>
            <td>Raceland</td>
            <td>LA</td>
            <td>303.0</td>
        </tr>
        <tr>
            <td>Cedars-Sinai Health System</td>
            <td>None</td>
            <td>CA</td>
            <td>303.0</td>
        </tr>
        <tr>
            <td>University of Louisville Hospital</td>
            <td>Louisville</td>
            <td>KY</td>
            <td>304.0</td>
        </tr>
        <tr>
            <td>St. Mary&#x27;s Regional Medical Center</td>
            <td>Lewiston</td>
            <td>ME</td>
            <td>305.0</td>
        </tr>
        <tr>
            <td>Jay Hospital</td>
            <td>Jay</td>
            <td>FL</td>
            <td>306.0</td>
        </tr>
        <tr>
            <td>Legacy Mount Hood Medical Center</td>
            <td>Gresham</td>
            <td>OR</td>
            <td>307.0</td>
        </tr>
        <tr>
            <td>St. Bernard Hospital</td>
            <td>Chicago</td>
            <td>IL</td>
            <td>308.0</td>
        </tr>
        <tr>
            <td>Pender Memorial Hospital</td>
            <td>Burgaw</td>
            <td>NC</td>
            <td>309.0</td>
        </tr>
        <tr>
            <td>Larkin Community Hospital Palm Springs Campus</td>
            <td>Hialeah</td>
            <td>FL</td>
            <td>310.0</td>
        </tr>
        <tr>
            <td>St. Luke&#x27;s Health - Patients Medical Center</td>
            <td>Pasadena</td>
            <td>TX</td>
            <td>311.0</td>
        </tr>
        <tr>
            <td>Ely Bloomenson Community Hospital</td>
            <td>Ely</td>
            <td>MN</td>
            <td>312.0</td>
        </tr>
        <tr>
            <td>Capital Region Medical Center</td>
            <td>Jefferson City</td>
            <td>MO</td>
            <td>313.0</td>
        </tr>
        <tr>
            <td>Mosaic Life Care at St. Joseph</td>
            <td>Saint Joseph</td>
            <td>MO</td>
            <td>314.0</td>
        </tr>
        <tr>
            <td>Tennova Healthcare-Lafollett Medical Center</td>
            <td>La Follette</td>
            <td>TN</td>
            <td>315.0</td>
        </tr>
        <tr>
            <td>White County Medical Center</td>
            <td>Searcy</td>
            <td>AR</td>
            <td>316.0</td>
        </tr>
        <tr>
            <td>Northwestern Medical Center Inc</td>
            <td>Saint Albans</td>
            <td>VT</td>
            <td>317.0</td>
        </tr>
        <tr>
            <td>Northern Hospital of Surry County</td>
            <td>Mount Airy</td>
            <td>NC</td>
            <td>318.0</td>
        </tr>
        <tr>
            <td>Bay Area Medical Center</td>
            <td>Marinette</td>
            <td>WI</td>
            <td>319.0</td>
        </tr>
        <tr>
            <td>T. J. Samson Community Hospital</td>
            <td>Glasgow</td>
            <td>KY</td>
            <td>320.0</td>
        </tr>
        <tr>
            <td>Northeast Georgia Medical Center Barrow</td>
            <td>Winder</td>
            <td>GA</td>
            <td>321.0</td>
        </tr>
        <tr>
            <td>Cape Coral Hospital</td>
            <td>Cape Coral</td>
            <td>FL</td>
            <td>322.0</td>
        </tr>
        <tr>
            <td>SSM Health St. Mary&#x27;s Hospital-Audrain</td>
            <td>Mexico</td>
            <td>MO</td>
            <td>323.0</td>
        </tr>
        <tr>
            <td>Merit Health Central</td>
            <td>Jackson</td>
            <td>MS</td>
            <td>324.0</td>
        </tr>
        <tr>
            <td>Vanderbilt Wilson County Hospital</td>
            <td>Lebanon</td>
            <td>TN</td>
            <td>325.0</td>
        </tr>
        <tr>
            <td>John C Stennis Memorial Hospital</td>
            <td>De Kalb</td>
            <td>MS</td>
            <td>326.0</td>
        </tr>
        <tr>
            <td>Saint James Hospital</td>
            <td>Pontiac</td>
            <td>IL</td>
            <td>327.0</td>
        </tr>
        <tr>
            <td>Houston Methodist San Jacinto Hospital</td>
            <td>Baytown</td>
            <td>TX</td>
            <td>328.0</td>
        </tr>
        <tr>
            <td>Boone County Hospital</td>
            <td>Boone</td>
            <td>IA</td>
            <td>329.0</td>
        </tr>
        <tr>
            <td>Oroville Hospital</td>
            <td>Oroville</td>
            <td>CA</td>
            <td>330.0</td>
        </tr>
        <tr>
            <td>Saint Alphonsus Medical Center - Nampa</td>
            <td>Nampa</td>
            <td>ID</td>
            <td>331.0</td>
        </tr>
        <tr>
            <td>Perry Memorial Hospital</td>
            <td>Perry</td>
            <td>OK</td>
            <td>332.0</td>
        </tr>
        <tr>
            <td>Community Hospital East</td>
            <td>Indianapolis</td>
            <td>IN</td>
            <td>333.0</td>
        </tr>
        <tr>
            <td>Scripps Mercy Hospital</td>
            <td>San Diego</td>
            <td>CA</td>
            <td>334.0</td>
        </tr>
        <tr>
            <td>Clinch Memorial Hospital</td>
            <td>Homerville</td>
            <td>GA</td>
            <td>335.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Washington</td>
            <td>Washington</td>
            <td>MO</td>
            <td>336.0</td>
        </tr>
        <tr>
            <td>HCA Houston Healthcare Northwest</td>
            <td>Houston</td>
            <td>TX</td>
            <td>337.0</td>
        </tr>
        <tr>
            <td>Paul B Hall Regional Medical Center</td>
            <td>Paintsville</td>
            <td>KY</td>
            <td>338.0</td>
        </tr>
        <tr>
            <td>Mayo Clinic Health System-New Prague</td>
            <td>New Prague</td>
            <td>MN</td>
            <td>339.0</td>
        </tr>
        <tr>
            <td>Hamilton Medical Center</td>
            <td>Dalton</td>
            <td>GA</td>
            <td>340.0</td>
        </tr>
        <tr>
            <td>Geisinger-Lewistown Hospital</td>
            <td>Lewistown</td>
            <td>PA</td>
            <td>341.0</td>
        </tr>
        <tr>
            <td>Panola Medical Center</td>
            <td>Batesville</td>
            <td>MS</td>
            <td>342.0</td>
        </tr>
        <tr>
            <td>AdventHealth Fish Memorial</td>
            <td>Orange City</td>
            <td>FL</td>
            <td>343.0</td>
        </tr>
        <tr>
            <td>Memorial Hospital</td>
            <td>Gonzales</td>
            <td>TX</td>
            <td>344.0</td>
        </tr>
        <tr>
            <td>Grady General Hospital</td>
            <td>Cairo</td>
            <td>GA</td>
            <td>345.0</td>
        </tr>
        <tr>
            <td>Mobile Infirmary Medical Center</td>
            <td>Mobile</td>
            <td>AL</td>
            <td>346.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital Jefferson</td>
            <td>Festus</td>
            <td>MO</td>
            <td>347.0</td>
        </tr>
        <tr>
            <td>Tristar Skyline Medical Center</td>
            <td>Nashville</td>
            <td>TN</td>
            <td>348.0</td>
        </tr>
        <tr>
            <td>Sharp Chula Vista Medical Center</td>
            <td>Chula Vista</td>
            <td>CA</td>
            <td>349.0</td>
        </tr>
        <tr>
            <td>Brandywine Hospital</td>
            <td>Coatesville</td>
            <td>PA</td>
            <td>350.0</td>
        </tr>
        <tr>
            <td>Marshfield Medical Center</td>
            <td>Marshfield</td>
            <td>WI</td>
            <td>351.0</td>
        </tr>
        <tr>
            <td>Siloam Springs Regional Hospital</td>
            <td>Siloam Springs</td>
            <td>AR</td>
            <td>352.0</td>
        </tr>
        <tr>
            <td>Lake City Community Hospital</td>
            <td>Lake City</td>
            <td>SC</td>
            <td>353.0</td>
        </tr>
        <tr>
            <td>Erie County Medical Center</td>
            <td>Buffalo</td>
            <td>NY</td>
            <td>354.0</td>
        </tr>
        <tr>
            <td>Advocate Condell Medical Center</td>
            <td>Libertyville</td>
            <td>IL</td>
            <td>355.0</td>
        </tr>
        <tr>
            <td>Inova Loudoun Hospital</td>
            <td>Leesburg</td>
            <td>VA</td>
            <td>356.0</td>
        </tr>
        <tr>
            <td>Wellstar Paulding Hospital</td>
            <td>Hiram</td>
            <td>GA</td>
            <td>357.0</td>
        </tr>
        <tr>
            <td>Highland CommunityÂ¬â€  Hospital</td>
            <td>Picayune</td>
            <td>MS</td>
            <td>358.0</td>
        </tr>
        <tr>
            <td>Kern Medical Center</td>
            <td>Bakersfield</td>
            <td>CA</td>
            <td>359.0</td>
        </tr>
        <tr>
            <td>Mercy Fitzgerald Hospital</td>
            <td>Darby</td>
            <td>PA</td>
            <td>360.0</td>
        </tr>
        <tr>
            <td>Weeks Medical Center</td>
            <td>Lancaster</td>
            <td>NH</td>
            <td>361.0</td>
        </tr>
        <tr>
            <td>Avera Queen of Peace</td>
            <td>Mitchell</td>
            <td>SD</td>
            <td>362.0</td>
        </tr>
        <tr>
            <td>SSM Health St. Mary&#x27;s Hospital - Jefferson City</td>
            <td>Jefferson City</td>
            <td>MO</td>
            <td>363.0</td>
        </tr>
        <tr>
            <td>St. Vincent Hospital</td>
            <td>Worcester</td>
            <td>MA</td>
            <td>364.0</td>
        </tr>
        <tr>
            <td>Indiana University Health Bedford Hospital</td>
            <td>Bedford</td>
            <td>IN</td>
            <td>365.0</td>
        </tr>
        <tr>
            <td>Promedica Bixby Hospital</td>
            <td>Adrian</td>
            <td>MI</td>
            <td>366.0</td>
        </tr>
        <tr>
            <td>Presence Mercy Medical Center</td>
            <td>Aurora</td>
            <td>IL</td>
            <td>367.0</td>
        </tr>
        <tr>
            <td>Mercy Hospital</td>
            <td>Moundridge</td>
            <td>KS</td>
            <td>368.0</td>
        </tr>
        <tr>
            <td>East Georgia Regional Medical Center</td>
            <td>Statesboro</td>
            <td>GA</td>
            <td>369.0</td>
        </tr>
        <tr>
            <td>Centracare Health - Monticello</td>
            <td>Monticello</td>
            <td>MN</td>
            <td>370.0</td>
        </tr>
        <tr>
            <td>Wayne County Hospital</td>
            <td>Monticello</td>
            <td>KY</td>
            <td>371.0</td>
        </tr>
        <tr>
            <td>Geary Community Hospital</td>
            <td>Junction City</td>
            <td>KS</td>
            <td>372.0</td>
        </tr>
        <tr>
            <td>Ascension Seton Hays</td>
            <td>Kyle</td>
            <td>TX</td>
            <td>373.0</td>
        </tr>
        <tr>
            <td>Taylor Regional Hospital</td>
            <td>Hawkinsville</td>
            <td>GA</td>
            <td>374.0</td>
        </tr>
        <tr>
            <td>Willamette Valley Medical Center</td>
            <td>McMinnville</td>
            <td>OR</td>
            <td>375.0</td>
        </tr>
        <tr>
            <td>Carilion Franklin Memorial Hospital</td>
            <td>Rocky Mount</td>
            <td>VA</td>
            <td>376.0</td>
        </tr>
        <tr>
            <td>Stoughton Hospital</td>
            <td>Stoughton</td>
            <td>WI</td>
            <td>377.0</td>
        </tr>
        <tr>
            <td>Osceola Regional Medical Center</td>
            <td>Kissimmee</td>
            <td>FL</td>
            <td>378.0</td>
        </tr>
        <tr>
            <td>Menifee Valley Medical Center</td>
            <td>Sun City</td>
            <td>CA</td>
            <td>379.0</td>
        </tr>
        <tr>
            <td>Emory Decatur Hospital</td>
            <td>Decatur</td>
            <td>GA</td>
            <td>380.0</td>
        </tr>
        <tr>
            <td>Memorial Medical Center</td>
            <td>Modesto</td>
            <td>CA</td>
            <td>381.0</td>
        </tr>
        <tr>
            <td>Belton Regional Medical Center</td>
            <td>Belton</td>
            <td>MO</td>
            <td>382.0</td>
        </tr>
        <tr>
            <td>Hillcrest Medical Center</td>
            <td>Tulsa</td>
            <td>OK</td>
            <td>383.0</td>
        </tr>
        <tr>
            <td>Conway Medical Center</td>
            <td>Conway</td>
            <td>SC</td>
            <td>384.0</td>
        </tr>
        <tr>
            <td>Lawrence General Hospital</td>
            <td>Lawrence</td>
            <td>MA</td>
            <td>385.0</td>
        </tr>
        <tr>
            <td>Morton Plant North Bay Hospital</td>
            <td>New Port Richey</td>
            <td>FL</td>
            <td>386.0</td>
        </tr>
        <tr>
            <td>Methodist Hospital</td>
            <td>Henderson</td>
            <td>KY</td>
            <td>387.0</td>
        </tr>
        <tr>
            <td>Adams County Regional Medical Center</td>
            <td>Seaman</td>
            <td>OH</td>
            <td>388.0</td>
        </tr>
        <tr>
            <td>Blount Memorial Hospital</td>
            <td>Maryville</td>
            <td>TN</td>
            <td>389.0</td>
        </tr>
        <tr>
            <td>Saint Anthony Medical Center</td>
            <td>Rockford</td>
            <td>IL</td>
            <td>390.0</td>
        </tr>
        <tr>
            <td>Ochsner LSU Health Shreveport</td>
            <td>Shreveport</td>
            <td>LA</td>
            <td>391.0</td>
        </tr>
        <tr>
            <td>Mary Washington Hospital</td>
            <td>Fredericksburg</td>
            <td>VA</td>
            <td>392.0</td>
        </tr>
        <tr>
            <td>St. Mary&#x27;s General Hospital</td>
            <td>Passaic</td>
            <td>NJ</td>
            <td>393.0</td>
        </tr>
        <tr>
            <td>Parkland Health Center</td>
            <td>Farmington</td>
            <td>MO</td>
            <td>394.0</td>
        </tr>
        <tr>
            <td>Jackson Memorial Hospital</td>
            <td>Miami</td>
            <td>FL</td>
            <td>395.0</td>
        </tr>
        <tr>
            <td>Midmichigan Medical Center-Clare</td>
            <td>Clare</td>
            <td>MI</td>
            <td>396.0</td>
        </tr>
        <tr>
            <td>Banner - University Medical Center Phoenix</td>
            <td>Phoenix</td>
            <td>AZ</td>
            <td>397.0</td>
        </tr>
        <tr>
            <td>Bon Secours Richmond Community Hospital</td>
            <td>Richmond</td>
            <td>VA</td>
            <td>398.0</td>
        </tr>
        <tr>
            <td>Wise Regional Health System</td>
            <td>Decatur</td>
            <td>TX</td>
            <td>399.0</td>
        </tr>
        <tr>
            <td>Doctors&#x27;Â¬â€  Community Hospital</td>
            <td>Lanham</td>
            <td>MD</td>
            <td>400.0</td>
        </tr>
        <tr>
            <td>Cuero Regional Hospital</td>
            <td>Cuero</td>
            <td>TX</td>
            <td>401.0</td>
        </tr>
        <tr>
            <td>Knapp Medical Center</td>
            <td>Weslaco</td>
            <td>TX</td>
            <td>402.0</td>
        </tr>
        <tr>
            <td>Methodist Fremont Health</td>
            <td>Fremont</td>
            <td>NE</td>
            <td>403.0</td>
        </tr>
        <tr>
            <td>SSM Health St. Clare Hospital - Baraboo</td>
            <td>Baraboo</td>
            <td>WI</td>
            <td>404.0</td>
        </tr>
        <tr>
            <td>North Sunflower Medical Center Cah</td>
            <td>Ruleville</td>
            <td>MS</td>
            <td>405.0</td>
        </tr>
        <tr>
            <td>The Washington Hospital</td>
            <td>Washington</td>
            <td>PA</td>
            <td>406.0</td>
        </tr>
        <tr>
            <td>Detroit Receiving Hospital &amp; University Health Center</td>
            <td>Detroit</td>
            <td>MI</td>
            <td>407.0</td>
        </tr>
        <tr>
            <td>Clay County Medical Center</td>
            <td>Clay Center</td>
            <td>KS</td>
            <td>408.0</td>
        </tr>
    </tbody>
</table>



 

Q6. Which organization type has the highest average equity rank?


```sql
%%sql 

SELECT TYPE_ForProfit AS 'For Profit Organization'
    , AVG([Tier 2_Equity Overall Rank]) AS 'Average Equity Rank'
FROM hospital_ranking
WHERE TYPE_ForProfit = 1
GROUP BY TYPE_ForProfit

UNION

SELECT TYPE_NonProfit AS 'For Profit Organization'
    , AVG([Tier 2_Equity Overall Rank]) AS 'Average Equity Rank'
FROM hospital_ranking
WHERE TYPE_NonProfit = 1
GROUP BY TYPE_NonProfit
;

```

     * sqlite:///lown_hospital.db
    Done.
    




<table>
    <thead>
        <tr>
            <th>For Profit Organization</th>
            <th>Average Equity Rank</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1</td>
            <td>1594.1571856287426</td>
        </tr>
        <tr>
            <td>1</td>
            <td>1669.2277823352474</td>
        </tr>
    </tbody>
</table>




```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```
