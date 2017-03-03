# restful
restful api for 3 years of weather data of cincinnati, ohio, US
http://35.165.137.243:5000/historical/
http://35.165.137.243:5000/historical/20130102
http://35.165.137.243:5000/historical/20201212,34,12
http://35.165.137.243:5000/historical/delete/20201212
historicalone - Return the whole database. all the dates and their respective temparatures.
historicaltwo - Return the maximium and minimum temparature of a specific date.
date not found - Return 404 error when the date searched is not present in the database
deletedvalue -  Deletes the entire information about a particular date
putValue - Inserts maximum and minimum temperatures of a particular date into the database
insertedvalue  -  after a value is inserted, the information about the values can be found out searching by date.
steps to do:
  
