# Exercise-11-API-Integration-and-Data-Processing
~~~
Name : W Allen Johnston Ozario  
Reg.No : 21222411004  
~~~

## Aim
To create a UiPath workflow that integrates with a REST API (e.g., Weather API), processes the returned JSON response, and writes specific data to a database or a structured format like Excel or CSV.

## Materials Required
UiPath Studio

Internet connection

Public REST API (e.g., OpenWeatherMap: https://api.openweathermap.org)

A valid API key (for APIs that require authentication)

UiPath.WebAPI.Activities (installed via Manage Packages)

UiPath.Database.Activities (optional if writing to DB)

Microsoft Excel or a local DB like SQLite

## Procedure
Step 1: Choose an API (e.g., Weather API)
Register at https://openweathermap.org/api and get a free API key.

Example API URL:
http://api.openweathermap.org/data/2.5/weather?q=Chennai&appid=your_api_key&units=metric

Step 2: Install WebAPI Activities
Go to Manage Packages → Official → Install UiPath.WebAPI.Activities.
Also install UiPath.JSON.Activities if not already present.

Step 3: Use HTTP Request Activity
Drag and drop the HTTP Request activity.

Set properties:
Method: GET
Endpoint: Paste the API URL with your key
Output: Create a variable responseJson (String)
Result: Check ResponseContent (output JSON as string)

Step 4: Deserialize JSON
Drag the Deserialize JSON activity.
Input: responseJson
Output: weatherData (JObject variable)

Step 5: Extract Required Values
Use Assign activities to extract data:

city = weatherData("name").ToString
temp = weatherData("main")("temp").ToString
condition = weatherData("weather")(0)("main").ToString
Create variables city, temp, and condition as Strings.

Step 6: Write to Database or Excel
Option A: Write to Excel/CSV
Use Build Data Table to structure columns: City, Temperature, Condition
Use Add Data Row to add the values.
Use Write Range to write the table to Excel or CSV.

Option B: Write to Database
Install and configure UiPath.Database.Activities
Use Insert activity to push data into an SQL table.

## OUTPUT:
For example, if API returns:

{
  "name": "Chennai",
  "main": {
    "temp": 33
  },
  "weather": [
    {"main": "Clouds"}
  ]
}
Your extracted values:

City: Chennai  
Temperature: 33°C  
Condition: Clouds
Will be written to Excel like:

City	Temperature	Condition
Chennai	33	Clouds

## Result
The UiPath workflow successfully calls a REST API, processes the JSON response, and writes the extracted weather data to a structured file (Excel/CSV) or database.

