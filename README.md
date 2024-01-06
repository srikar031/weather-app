# weather-app
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <title>Weather App Using OpenWeatherMap API</title>

    <link rel="icon" type="image/x-icon" href="icons/favicon.ico">

    <link rel="stylesheet" href="styles/style.css">
    <link rel="prefetch" href="media/day1.jpg">
    <link rel="prefetch" href="media/day2.jpg">
    <link rel="prefetch" href="media/day3.jpg">
    <link rel="prefetch" href="media/day4.jpg">
    <link rel="prefetch" href="media/day5.jpg">
    <link rel="prefetch" href="media/night1.jpg">
    <link rel="prefetch" href="media/night2.jpg">
    <link rel="prefetch" href="media/night3.jpg">
    <link rel="prefetch" href="media/night4.jpg">
    <link rel="prefetch" href="media/night5.jpg">
    <link rel="prefetch" href="media/rainy1.jpg">
    <link rel="prefetch" href="media/rainy2.jpg">
    <link rel="prefetch" href="media/rainy3.jpg">
    <link rel="prefetch" href="media/rainy4.jpg">
    <link rel="prefetch" href="media/rainy5.jpg">
    <link rel="prefetch" href="media/cloudy1.jpg">
    <link rel="prefetch" href="media/cloudy2.jpg">
    <link rel="prefetch" href="media/cloudy3.jpg">
    <link rel="prefetch" href="media/cloudy4.jpg">
    <link rel="prefetch" href="media/cloudy5.jpg">
    <link rel="prefetch" href="icons/loader.gif">

    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@500&display=swap" rel="stylesheet">

    <style>
      body
      {
        /* background-image: linear-gradient(rgba(0, 0, 0, 0.5),rgba(0, 0, 0, 0.5)) , url('media/day1.jpg'); */
        -webkit-background-size: cover;
        -moz-background-size: cover;
        -o-background-size: cover;
        
        /* Added background-repeat and set it to no-repeat to help prevent the images from duplicating. I added !important to 
         * background-repeat and background-size in order to place importance on the background images not repeating and
         * to cover the entire webpage. Phillip Andrews
         */
        background-repeat: no-repeat !important;
        background-size: cover !important;
        background-attachment: fixed;

				height: 100vh;
      }
			@media (max-width: 600px)
			{
				body
				{
					height: 100%;
				}
			}
    </style>
  </head>
  <body>
    <ul class="navbar">
      <li style="float: left; margin-left: -10px;" class="forecast"><a class="repo-link" href="https://github.com/kshitizrohilla/weather-app-using-openweathermap-api/">⛄ Forecast</a></li>
      <li><a href="#">⟳</a></li>
      <li><a href="#">☆<!--★--></a></li>
      <li><a href="#">···</a></li>
      <li><input spellcheck="false" class="search-city" id="searchCity" type="text" autocomplete="off" placeholder="🔍︎ Search City"></li>
    </ul>

		<ul class="mobile-navbar">
      <li><input spellcheck="false" class="mobile-search-city" id="mobileSearchCity" type="text" autocomplete="off" placeholder="Search City..."></li>
    </ul>

    <h1 class="location-name" id="locationName">Search City...</h1>

    <div class="temperature-container">
      <div class="temperature-icon"><img class="imgs-as-icons" src="icons/sunny.png"></div>
      <div class="temperature-value" id="temperatureValue"></div>
    </div>

    <h2 class="weather-type" id="weatherType"></h2>

    <div class="additionals-first-row">
      <span class="air-quality-additional">
        <span class="air-quality-additional-label">Air Quality Index </span>
        <span class="air-quality-index-additional-value">Moderate</span>
      </span>

      <span class="real-feel-additional">
        <span class="real-feel-additional-label">Real Feel </span>
        <span class="real-feel-additional-value" id="realFeelAdditionalValue">-</span>
      </span>

      <span class="humidity-additional">
        <span class="humidity-additional-label">Humidity </span>
        <span class="humidity-additional-value" id="humidityAdditionalValue">-</span>     
      </span>

      <span class="max-temperature-additional">
        <span class="max-temperature-additional-label">Highest Temperature </span>
        <span class="max-temperature-additional-value" id="maxTemperatureAdditionalValue">-</span>
      </span>

      <span class="min-temperature-additional">
        <span class="min-temperature-additional-label">Lowest Temperature </span>
        <span class="min-temperature-additional-value" id="minTemperatureAdditionalValue">-</span>          
      </span>
    </div>

    <div class="additionals-second-row">
      <span class="wind-speed-additional">
        <span class="wind-speed-additional-label">Wind Speed </span>       
        <span class="wind-speed-additional-value" id="windSpeedAdditionalValue">-</span>
      </span>

      <span class="wind-direction-additional">
        <span class="wind-direction-additional-label">Wind Direction </span>
        <span class="wind-direction-additional-value" id="windDirectionAdditionalValue">-</span>
      </span>

      <span class="visibility-additional">
        <span class="visibility-additional-label">Visibility </span>
        <span class="visibility-additional-value" id="visibilityAdditionalValue">-</span>
      </span>

      <span class="pressure-additional">
        <span class="pressure-additional-label">Pressure </span>       
        <span class="pressure-additional-value" id="pressureAdditionalValue">-</span>
      </span>

      <span class="sunrise-additional">
        <span class="sunrise-additional-label">Sunrise </span>
        <span class="sunrise-additional-value" id="sunriseAdditionalValue">-</span>  
      </span>

      <span class="sunset-additional">
        <span class="sunset-additional-label">Sunset </span>
        <span class="sunset-additional-value" id="sunsetAdditionalValue">-</span>
      </span>
    </div>

    <br>
    <!-- <div class="separator"></div> -->

    <div class="daily-forecast">

      <h2 class="daily-forecast-label">Daily</h2>

      <div class="daily-forecast-card">
        <p class="daily-forecast-date">Fri 27</p>
        <div class="daily-forecast-logo"><img class="imgs-as-icons" src="icons/sunny.png"></div>
        <div class="max-min-temperature-daily-forecast">
          <span class="max-daily-forecast">37<sup>o</sup>C</span>
          <span class="min-daily-forecast">25<sup>o</sup>C</span>
        </div>
        <p class="weather-type-daily-forecast">Sunny</p>
      </div>

      <div class="daily-forecast-card">
        <p class="daily-forecast-date">Fri 27</p>
        <div class="daily-forecast-logo"><img class="imgs-as-icons" src="icons/sunny.png"></div>
        <div class="max-min-temperature-daily-forecast">
          <span class="max-daily-forecast">37<sup>o</sup>C</span>
          <span class="min-daily-forecast">25<sup>o</sup>C</span>
        </div>
        <p class="weather-type-daily-forecast">Sunny</p>
      </div>

      <div class="daily-forecast-card">
        <p class="daily-forecast-date">Fri 27</p>
        <div class="daily-forecast-logo"><img class="imgs-as-icons" src="icons/sunny.png"></div>
        <div class="max-min-temperature-daily-forecast">
          <span class="max-daily-forecast">37<sup>o</sup>C</span>
          <span class="min-daily-forecast">25<sup>o</sup>C</span>
        </div>
        <p class="weather-type-daily-forecast">Sunny</p>
      </div>

      <div class="daily-forecast-card">
        <p class="daily-forecast-date">Fri 27</p>
        <div class="daily-forecast-logo"><img class="imgs-as-icons" src="icons/sunny.png"></div>
        <div class="max-min-temperature-daily-forecast">
          <span class="max-daily-forecast">37<sup>o</sup>C</span>
          <span class="min-daily-forecast">25<sup>o</sup>C</span>
        </div>
        <p class="weather-type-daily-forecast">Sunny</p>
      </div>

      <div class="daily-forecast-card">
        <p class="daily-forecast-date">Fri 27</p>
        <div class="daily-forecast-logo"><img class="imgs-as-icons" src="icons/sunny.png"></div>
        <div class="max-min-temperature-daily-forecast">
            <span class="max-daily-forecast">37<sup>o</sup>C</span>
            <span class="min-daily-forecast">25<sup>o</sup>C</span>
        </div>
        <p class="weather-type-daily-forecast">Sunny</p>
      </div>

      <div class="daily-forecast-card">
        <p class="daily-forecast-date">Fri 27</p>
        <div class="daily-forecast-logo"><img class="imgs-as-icons" src="icons/sunny.png"></div>
        <div class="max-min-temperature-daily-forecast">
          <span class="max-daily-forecast">37<sup>o</sup>C</span>
          <span class="min-daily-forecast">25<sup>o</sup>C</span>
        </div>
        <p class="weather-type-daily-forecast">Sunny</p>
      </div>
    </div>
    
    <script src="scripts/script.js"></script>
		<script src="scripts/mobile.js"></script>
		<br><br><br><br><br>
  </body>
</html>
