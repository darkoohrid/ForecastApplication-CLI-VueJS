# ForecastApplication-CLI-VueJS

Simple VueJS-cli Forecast Application obtaining data from OpenWeatherMap API for city Maribor , having coordinates as input (lat=46.55&lon=15.64).
Displaying the data in the application, with possibility to reload the data on a button with timestamp display.

API - https://api.openweathermap.org/data/2.5/onecall?lat=46.55&lon=15.64&units=metric&exclude=hourly,minutely&appid={api_key}

-Things to be implemented in future:
1. Instead of “Maribor” as city, display the forecast for the user's current location. (also Implementing a Map reading coordinates from click can be interesting).
2. Responsivness (bootstrap, scss, mediaqueries).
3. Translate the application in real time using the i18n library. Export all the keys for later translation. The browser language should affect the display of the date format.
