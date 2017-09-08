# Show-the-Local-Weather
FreeCodeCamp intermediate front end development project - Show the Local Weather
link: https://www.freecodecamp.org/challenges/show-the-local-weather

link to my codepen: https://codepen.io/CarlisleLiu/pen/zdEomX

```
HTML
<body>
  <h1>Local Weather</h1>
  <p>This is a <a href = "https://www.freecodecamp.org/challenges/show-the-local-weather" target = "_blank">FreeCodeCamp Intermediate Front End Development Project</a>. The data is provided by <a href = "https://fcc-weather-api.glitch.me" target = "_blank">FCC weather API.</a></p>
  <div>
    <h2 id = "weather"></h2>
    <img id = "icon"></img>
    <p><span id = "temp"></span> <span id = "tempUnit"></span></p>
    <span>(Press the unit to switch between Celsius and Fehrenheit temperatures)</span>
  </div>
  
<footer>
    <ul>
      <li id = "copyRights" style = "float:left; font-size: 15px; margin: 10px 0 0">Carlisle_Liu 2017 All Rights Reserved</li>
      <li id = "myFacebook" style = "float:right; font-size: 25px; margin: 0 15px" target = "_blank"><a href = "https://www.facebook.com/profile.php?id=100002255286950" target = "_blank"><i class = "fa fa-facebook-official" style = "color:black"></i></a></li>
      <li id = "myTwitter" style = "float:right; font-size: 25px; margin: 0 15px" target = "_blank"><a href = "https://twitter.com/Carlisle_Liu" target = "_blank"><i class = "fa fa-twitter" style = "color:black"></i></a></li>
      <li id = "myGithub" style = "float:right; font-size: 25px; margin: 0 15px" target = "_blank"><a href = "https://github.com/Carlisleliu" target = "_blank"><i class = "fa fa-github-square" style = "color:black"></i></a></li>
    </ul>
</footer>
</body>


CSS
body {
  text-align: center;
  background-image: url("http://4.bp.blogspot.com/-G9l0fEJS-G4/VehcqkFmRrI/AAAAAAAAkaE/3cSjNCmvtKY/s1600/maxresdefault.jpg");
  opacity: 0.95;
}

h1 {
  margin-top: 50px;
  margin-bottom: 20px;
}

#weather {
  margin-top: 50px;
}

div p {
  font-size: 25px;
  text-transform: capitalize;
}

img {
  height: 130px;
  width: 130px;
}

#tempUnit {
  cursor: pointer;
}

footer {
  position: fixed;
  right: 0;
  left: 0;
  bottom: 0;
  font-color: #000000;
  height: 35px;
  width: 100%;
  font-weight: 300;
}

ul{
  list-style-type: none;
  display: block;
  margin: 0 0 0 10px;
  padding: 0;
}


Javascript
$(document).ready(function() {
  var currentTemp
  
  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(function(position) {
      var lat = "lat=" + (Math.round(position.coords.latitude * 10) / 10);
      var lon = "&lon=" + (Math.round(position.coords.longitude * 10) / 10);
      var api = "https://fcc-weather-api.glitch.me/api/current?" + lat + lon;
      localWeather(api);
    })
  }
  
  function localWeather(api) {
  $.ajax({
    url: api,
    success: function(data) {
      $("h2").html(data.name + ", " + data.sys.country);
      $("img").attr("src", data.weather[0].icon);
      $("#temp").html(Math.round(data.main.temp * 10) / 10);
      $("#tempUnit").html("\xB0C");
      currentTemp = data.main.temp;
    }
  });
  }
  
  
  $("#tempUnit").click(function() {
    var currentTempUnit = $("#tempUnit").html() == "\xB0C" ? "\xB0F" : "\xB0C";
    $("#tempUnit").html(currentTempUnit);
    if (currentTempUnit == "\xB0F") {
      var fahTemp = (Math.round((currentTemp * (9 / 5) + 32) * 10) / 10);
      $("#temp").html(fahTemp);
    }
    else {
      $("#temp").html(Math.round(currentTemp * 10) / 10);
    }
  });
  
});
```
