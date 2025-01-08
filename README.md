# project3_group4
Output of the project 3 - group 4 
Members : nazim bendjaballah


1) objective
How a country’s macroeconomic indicators affects Immigration to Canada

To visualize and explore different country macroeconomic indicators and assess whether or not it is a good indicator for immigration to Canada
To analyze how GDP impacts immigration rates to Canada from different countries.
To identify trends and correlations between economic strength (measured by GDP) and immigration flows.
To present insights visually and dynamically for better interpretation and decision-making.


2) Organization of the repository

Main directory
    Data_collection jupyter notebook : code to extract, transform and load data
    visualizations jupyter notebook : code to generate charts and analysis
    create_db jupyter notebook : code to create the SQLITE db
    immigration_db.sqlite : database created from data collected
    app_project : API to access data
    visualization_leaflets.html : javascript for leaflet visualization
    visualization_other_outputs : outputs of the different charts 

Output directory
    csv files generated by collection and transformation step
    png file with the EDB
    pg files with charts
    GIF file with the race chart

others directory
    doc : proposal of the project
    ppt : final presentation


3) DATA COLLECTION AND TRANSFORMATION
use jupyter notebook : Data_collection.ipynb
 
Dependencies used

    - import pandas as pd
    - import pathlib as path
    - import requests
    - import json
    - from pprint import pprint
    - import numpy as np
    - from scipy.stats import linregress
    - from io import StringIO


3.1) data collection
    3.1.1) for immigration data 
        source : Immigration, refugees and citizenship of Canada
        type : CSV file
        Access : https://www.ircc.canada.ca/opendata-donneesouvertes/data/ODP-PR-Citz.csv

    3.1.2) for macro-economic data 
        source : World bank
        type : API
        Access : https://api.worldbank.org/v2/country/XXX/indicator/XX.XXX.XXX.XX?date=XXXX:XXXX&format=json

        3.1.2.1) countries
        countries are selected from immigration list merged with countries to extract the iso3code Example Canada = CAN
        3.1.2.2) indicators
        you can add any indicator a the list . this list will be used to loop

    3.1.3) We need an intermediate data to link the country name (in immigration data) and country code (used by the API)
        this link is provided by a datafram countries 
        source : World bank
        type : API
        Access : https://api.worldbank.org/v2/country?format=json


3.2) data cleaning and transformation

    3.2.1) countries data
        - drop rows with nan representing regions
        - change type of data

    3.2.2) immigration data
        - drop columns in frensh
        - data type conversion
        - replace empty values
        - replace NAN values
        - replace country name : the names used in the 2 datasets do not match
            => identify the mismatch and manually create a mapping dictionary 
            =>  replace 78 countries to be in line with World bank
        - rename columns

        - map months to get the numeric value (exp : mars : 3, apr : 4)

        - reset index

        - group by function to generate 2 df : immigration by country + immigration by country and by year

    3.2.2) macroeconomic data
        - retrieve countries list from immigration
        - 
        : drop and rename columns after merge
        - change data type



3.3) output
    csv countries_list_UN_referential: Countries list United Nations referential 
    csv immigrants_by_country_monthly: immigration by country and by month from 2015 to 2024
    csv : immigration cumulated by country from 2015 to 2024
    csv : immigration by country and by year from 2015 to 2024
    csv macro_economic_data: selected indicators for each country and by year from 2015 to 2024


4) DATABASE creation
use jupyter notebook : create_db.ipynb
output : database sqlite : immigration_canada_pr.sqlite
output : quick DBD png file : QuickDBD-export.png

Dependencies used
    # Import SQL Alchemy
    from sqlalchemy import create_engine

    # Import and establish Base for which classes will be constructed
    from sqlalchemy.ext.declarative import declarative_base


    # Import modules to declare columns and column data types
    from sqlalchemy import Column, Integer, String, Float, Boolean, MetaData, Table

    # Import the Python SQL toolkit and Object Relational Mapper
    import sqlalchemy
    from sqlalchemy.ext.automap import automap_base
    from sqlalchemy.orm import Session
    from sqlalchemy import create_engine, inspect

- use of declarative_base method

- table creation
    - 3 tables
    - creation of 3 classes : countries, immigration, macrodata

- data importation
importation of data with function tosql() from the csv files generated in step 1


5) API use jupyter notebook : Data_collection.ipynb

use python file : app_project.py
on sqlite db created in step 2

# Import the dependencies.

    import sqlalchemy
    from sqlalchemy.ext.automap import automap_base
    from sqlalchemy.orm import Session
    from sqlalchemy import create_engine, func
    import numpy as np
    from datetime import timedelta, datetime
    from dateutil.relativedelta import relativedelta
    from flask import Flask, jsonify   
    from collections import defaultdict  # to generate dictionary 'precipitation


- use of automap_base method

- create a server : http://127.0.0.1:5000 : it describes the possibilities

- create 6 links to extract data 

6) visualizations
2 html files
visualization_leaflets : world map of the immigration flow with LEAFLET
visualization _ outputs : 3 charts among them a race chart bar


leaflet
    the JS code is in file project3_group4\static\js\logic.js
    uses the route http://127.0.0.1:5000/api/v0.1/immigation_flow_per_country

        <!-- Leaflet JS -->
        "https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"
        integrity="sha256-20nQCchB9co0qIjJZRGuk2/Z9VM+kNiyxNV1lvTlZBo="
        crossorigin="">
    <!-- Leaflet MarkerCluster JS -->
    script src="https://unpkg.com/leaflet.markercluster@1.5.3/dist/leaflet.markercluster.js"
    <!-- D3 JavaScript -->
    script src="https://d3js.org/d3.v7.min.js"
    <!-- Our JavaScript -->
    script type="text/javascript" src="static/js/logic.js"

6) external codes used
for generation of the race bar chart
source : https://github.com/dexplo/bar_chart_race
Library bar_chart_race : bar_chart_race (pip install bar_chart_race)
documentation : https://www.dexplo.org/bar_chart_race/tutorial/

7) publishing
the outpu is published in github repository
https://nazimben25.github.io/project3_group4/