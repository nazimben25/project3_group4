# project3_group4
Output of the project 3 - group 4 
Members : talal sidiki , nazim bendjaballah


1) objective
How a country’s macroeconomic indicators affects Immigration to Canada

To visualize and explore different country macroeconomic indicators and assess whether or not it is a good indicator for immigration to Canada
To analyze how GDP impacts immigration rates to Canada from different countries.
To identify trends and correlations between economic strength (measured by GDP) and immigration flows.
To present insights visually and dynamically for better interpretation and decision-making.

2) DATA COLLECTION AND TRANSFORMATION
2.1) data collection
    2.1.1) for immigration data 
        source : Immigration, refugees and citizenship of Canada
        type : CSV file
        Access : https://www.ircc.canada.ca/opendata-donneesouvertes/data/ODP-PR-Citz.csv

    2.1.2) for macro-economic data 
        source : World bank
        type : API
        Access : https://api.worldbank.org/v2/country/XXX/indicator/XX.XXX.XXX.XX?date=XXXX:XXXX&format=json

        2.1.2.1) countries
        countries are selected from immigration list merged with countries to extract the iso3code Example Canada = CAN
        2.1.2.2) indicators
        you can add any indicator a the list . this list will be used to loop

    2.1.3) We need an intermediate data to link the country name (in immigration data) and country code (used by the API)
        this link is provided by a datafram countries 
        source : World bank
        type : API
        Access : https://api.worldbank.org/v2/country?format=json


2.2) data cleaning and transformation



    2.2.1) immigration data
        - drop columns in frensh
        - data type conversion
        - replace empty values
        - replace NAN values
        - replace country name
        - rename columns
        - map months to get the numeric value
        - split column valu to eliminate extra strings
        - change data type
        - drop additional columns
        - reset index
        - change name of countries to be in line with UN convention (45 countries)

        - group by function to generate 2 df : immigration by country + immigration by country and by year

    2.2.2) macroeconomic data
        - retrieve countries list from immigration
        - 

        : drop and rename columns after merge
        - change data type

    2.2.3) countries data
        - drop rows with nan representing regions
        - change type of data

2.3) output
    csv : Countries list United Nations referential 
    csv : immigration cumulated by country from 2015 to 2024
    csv : immigration by country and by year from 2015 to 2024
    csv : selected indicatos for each country and by year from 2015 to 2024


3) DATABASE creation


4) API 