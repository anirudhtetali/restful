# restful
restful api for 3 years of weather data of cincinnati, ohio, US

All Dates                 - http://35.165.137.243:5000/historical/
See about Particular date - http://35.165.137.243:5000/historical/20130102
Insert info. about date   - http://35.165.137.243:5000/historical/20201212,34,12
Delete info. about date   - http://35.165.137.243:5000/historical/delete/20201212

Information about images.
historicalone   - Return the whole database. all the dates and their respective temparatures.
historicaltwo   - Return the maximium and minimum temparature of a specific date.
date not found  - Return 404 error when the date searched is not present in the database
deletedvalue    - Deletes the entire information about a particular date
putValue        - Inserts maximum and minimum temperatures of a particular date into the database
insertedvalue   - after a value is inserted, the information about the values can be found out searching by date.

Tools needed:
  Flask, python, sqlite, flask-restful, curl
  
Steps to do:
1. save the app.py file and run it in your local host (127.0.0.1) or public IP.
2. Port is 5000
3. End points:
  a.  /historical/                - all dates and their information.
  b.  /historical/date            - GET method will return information about that particular date.
  c.  /historical/date            - Delete method will delete the information about that particular date.
  d.  /historical/date,tmax,tmin  - Inserts information about a new date into database.
 
