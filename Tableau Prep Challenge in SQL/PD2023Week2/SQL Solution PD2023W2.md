
**2023: Week 2 - International Bank Account Numbers**
-------------------

January 11, 2023  
Challenge By: Jenny Martin

For week 2 of our beginner month, Data Source Bank has a requirement to construct International Bank Account Numbers (IBANs), even for Transactions taking place in the UK. We have all the information in separate fields, we just need to put it altogether in the following order:
![image](https://github.com/shresnit/SQL-Projects/assets/100710335/228d106b-7b48-46da-807f-8fd48afc8465)




**Requirements**  
- Input the data
- In the Transactions table, there is a Sort Code field which contains dashes. We need to remove these so just have a 6 digit string 
- Use the SWIFT Bank Code lookup table to bring in additional information about the SWIFT code and Check Digits of the receiving bank account 
- Add a field for the Country Code 
  - Hint: all these transactions take place in the UK so the Country Code should be GB
- Create the IBAN as above 
  - Hint: watch out for trying to combine sting fields with numeric fields - check data types
- Remove unnecessary fields 
- Output the data

<br>
<br>

**SQL Solution** (*In Snowflake*)

    SELECT T.TRANSACTION_ID,
            CONCAT('GB' ||
                    S.CHECK_DIGITS ||
                    S.SWIFT_CODE ||
                    regexp_replace(T.sort_code, '-', '') ||
                    T.ACCOUNT_NUMBER
                    ) AS IBAN
    FROM PD2023_WK02_TRANSACTIONS AS T
    INNER JOIN PD2023_WK02_SWIFT_CODES AS S
        ON T.BANK = S.BANK
    ;

**Result**
|TRANSACTION_ID|IBAN                  |
|--------------|----------------------|
|3888          |GB12DSBX95988262230725|
|7423          |GB22HLFX49312675616805|
|3286          |GB22HLFX21853047326725|
|6764          |GB12DSBX29723910570182|
|2021          |GBC1LOYD59175172261023|
|9373          |GB4BHBUK24151244568613|
|7983          |GB2LNWBK67189758775796|
|8813          |GBC1LOYD63589183475180|
|3270          |GB2LNWBK16710742126094|
|2868          |GB4BHBUK81899653579089|
|9195          |GB22BARC29369996432979|
|2797          |GB22HLFX36632147474979|
|9096          |GB4BHBUK74259532710603|
|7485          |GBC1LOYD63461763007765|
|2340          |GB4BHBUK95741982753835|
|7268          |GB2LNWBK88752496412639|
|8629          |GB2LNWBK65358083955552|
|9530          |GB12DSBX70700574379515|
|2953          |GB22BARC16157480259094|
|1062          |GB22BARC75189450400945|
|9224          |GB4BHBUK58346132950330|
|2760          |GB12DSBX28066085744933|
|3598          |GB2LNWBK93263053420865|
|6999          |GB2LNWBK79647546226858|
|5834          |GB2LNWBK73789035061906|
|7665          |GB22BARC97774786932953|
|8808          |GB4BHBUK97038541599267|
|3770          |GB12DSBX32549026013637|
|1281          |GB2LNWBK42252795862106|
|5773          |GBC1LOYD43861382021377|
|4653          |GB22HLFX98290826844967|
|1215          |GB22BARC86447625328896|
|1614          |GB22HLFX69112538668066|
|6054          |GBC1LOYD96885447199472|
|8500          |GBC1LOYD87493846967961|
|5955          |GBC1LOYD97849671124764|
|7081          |GB4BHBUK99836025862478|
|2354          |GB22BARC23881843602961|
|9760          |GB4BHBUK90535525504883|
|8864          |GB3EABBY43622091658439|
|1716          |GB3EABBY68363652310258|
|8453          |GBC1LOYD64945830335066|
|3600          |GB22HLFX33530821348995|
|6155          |GB4BHBUK24815290692776|
|1730          |GB22BARC49536476275760|
|4063          |GB12DSBX28178620220923|
|2570          |GB22BARC20766392497278|
|4856          |GB4BHBUK74721138183636|
|2031          |GB3EABBY73485061059913|
|2902          |GB4BHBUK67357062609049|
|9415          |GB3EABBY44478144418182|
|9307          |GB2LNWBK34762822610455|
|7809          |GB2LNWBK19611433725878|
|9137          |GB12DSBX41316078873999|
|4102          |GB22HLFX59660150508460|
|4251          |GB22HLFX64482127270504|
|4756          |GB3EABBY26638594377199|
|6933          |GB3EABBY41192656478271|
|4060          |GB2LNWBK58372337658820|
|4859          |GB4BHBUK66307466763721|
|2882          |GB4BHBUK43474072954282|
|1952          |GB12DSBX21275453786334|
|7353          |GB22HLFX13766021915880|
|4580          |GB22HLFX24729957383660|
|1327          |GB3EABBY25318860934362|
|8403          |GB2LNWBK29270985946847|
|1126          |GBC1LOYD45825569969270|
|3890          |GB3EABBY70037475951736|
|5778          |GB3EABBY75783470255646|
|7066          |GB3EABBY54100385919526|
|9181          |GB22BARC96924067860804|
|6948          |GB22HLFX16586513213297|
|9992          |GB4BHBUK71694010170574|
|1673          |GB22HLFX92575259488515|
|5042          |GB4BHBUK23914453092685|
|3892          |GB3EABBY23651853393048|
|3279          |GB4BHBUK34843258721386|
|1572          |GB4BHBUK88532572219605|
|8110          |GB3EABBY65905240072077|
|8664          |GB3EABBY21090451052559|
|5644          |GB22BARC21841777656886|
|1493          |GB12DSBX86544212193988|
|2774          |GB4BHBUK57548710519002|
|1314          |GB12DSBX61857971210735|
|1425          |GB4BHBUK74789296930299|
|7778          |GB22BARC55073838687214|
|4870          |GBC1LOYD51074179724968|
|6400          |GB3EABBY80436238383736|
|3959          |GB22BARC35598782773607|
|7086          |GB12DSBX59774456630552|
|1298          |GB3EABBY42635630601237|
|5574          |GB22HLFX10019840722610|
|1671          |GB4BHBUK19554477144031|
|9741          |GB4BHBUK56593943638730|
|1245          |GB4BHBUK50846668373125|
|4656          |GB22BARC79827460830548|
|2535          |GB22BARC57143268745993|
|9013          |GB2LNWBK93877113350031|
|5404          |GB22BARC53282134302539|
|4746          |GB22BARC42863883172326|
