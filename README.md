# ForecastApplication-CLI-VueJS

VueJS-cli Forecast Application obtaining data from OpenWeatherMap API , having coordinates as input (default: lat=46.55&lon=15.64, Maribor), option to enter any input, or get your current location.
Displaying the data in the application, with possibility to reload the data on a button with timestamp display.

API - https://api.openweathermap.org/data/2.5/onecall?lat=46.55&lon=15.64&units=metric&exclude=hourly,minutely&appid={api_key}

-Things to be implemented in future:
1. Responsivness (bootstrap, scss, mediaqueries).
2. Translate the application in real time using the i18n library. Export all the keys for later translation. The browser language should affect the display of the date format.
3. Implement a Map for user to select a specific place and show the temperature there.

Photo of current version:
![WeatherForecastAppSS](https://user-images.githubusercontent.com/82602862/141869295-bade3774-95fd-4c9b-bb74-7d2ae3844215.png)
