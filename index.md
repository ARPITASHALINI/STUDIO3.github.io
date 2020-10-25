<html>
    <head>
        <script src='https://api.mapbox.com/mapbox-gl-js/v1.12.0/mapbox-gl.js'></script>
        <link href='https://api.mapbox.com/mapbox-gl-js/v1.12.0/mapbox-gl.css' rel='stylesheet' /> 
        <script> mapboxgl.accessToken = 'pk.eyJ1IjoiYXJwaXRhMjUwOSIsImEiOiJja2dibnVxenQwMHUxMnptZjJjZ2dqNnRpIn0.k-hGdFzGPxjJ1CbQP10D3w'; </script>
        <style>
            body {
              margin: 0;
              padding: 0;
            }

   h2,
   h3 {
   margin: 10px;
   font-size: 1.2em;
 }

h3 {
  font-size: 1em;
}

p {
  font-size: 0.85em;
  margin: 10px;
  text-align: center;
}

/**
* Create a position for the map
* on the page */
#map {
  position: absolute;
  top: 250px;
  bottom: 0;
  width: 75%;
  border-style: inset;
  height: 650px;
  margin: 50px
}
body {
  background-color: #f0d9dd;
}
ul {
  background: #FCF3CF;
  padding: 40px;
  width: 20%;
  position: absolute;
  text-align: center;
  display: inline-block;
  margin: 20px;
  zoom:1;
  display: inline;
  vertical-align: middle;
}
ul li{
  display: inline;
  text-align: center;
  vertical-align: middle;
}

/**
* Set rules for how the map overlays
* (information box and legend) will be displayed
* on the page. */
.map-overlay {
  position: absolute;
  bottom: 0;
  right: 0;
  background: rgba(255, 255, 255, 0.8);
  margin-right: 20px;
  font-family: Arial, sans-serif;
  overlay: auto;
  border-radius: 3px;
}

#features {
  top: 275px;
  height: 200px;
  margin-top: 0px;
  width: 195px;
  margin: 60px;
  position: absolute;
}

 #legend {
  padding: 10px;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  line-height: 18px;
  height: 200px;
  margin-bottom: 20px;
  width: 100px;
  margin-top: 450px;
}

.legend-key {
  display: inline-block;
  border-radius: 20%;
  width: 10px;
  height: 10px;
  margin-right: 5px;
}
        </style>
    </head>
    <body>
      <h1 style="font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif; text-align: center;">Studio Week 3<br> Interaction with Mapbox GL JS </h1>
      <ul>
        <li><a href="index.html" target="_self" style="color: #09166c"> &raquo; Output 1</a></li>
        <li><a class="active" href="mapbox-interaction.html" target="_self" style="color: #09166c"> &raquo; Output 2</a></li>
        <li><a href="mapbox-turfjs.html" target="_self" style="color: #09166c"> &raquo; Output 3</a></li>
      </ul>
        <div id='map'></div>
        <div class='map-overlay' id='features'><h2>US population density</h2><div id='pd'><p>Hover over a state!</p></div></div>
        <div class='map-overlay' id='legend'></div>
        <script>
          
        var map = new mapboxgl.Map({
            container: 'map', // container id
            style: 'mapbox://styles/arpita2509/ckgikmrhh1vzk19pjrrb6n42z' // replace this with your style URL
          });
          
          map.on('load', function() {
            var layers = ['0-10', '10-20', '20-50', '50-100', '100-200', '200-500', '500-1000', '1000+'];
            var colors = ['#FFF7F3', '#FDE0DD', '#FCC5C0', '#FA9FB5', '#F768A1', '#DD3497', '#AE017E', '#7A0177'];
            for (i = 0; i < layers.length; i++) {
                var layer = layers[i];
                var color = colors[i];
                var item = document.createElement('div');
                var key = document.createElement('span');
                key.className = 'legend-key';
                key.style.backgroundColor = color;

                var value = document.createElement('span');
                value.innerHTML = layer;
                item.appendChild(key);
                item.appendChild(value);
                legend.appendChild(item);
            }
            map.on('mousemove', function(e) {
            var states = map.queryRenderedFeatures(e.point, {
            layers: ['statedata']
            });

            if (states.length > 0) {
                document.getElementById('pd').innerHTML = '<h3><strong>' + states[0].properties.name + '</strong></h3><p><strong><em>' + states[0].properties.density + '</strong> people per square mile</em></p>';
                } else {
                document.getElementById('pd').innerHTML = '<p>Hover over a state!</p>';
                }
            });
            map.getCanvas().style.cursor = 'default';
            map.fitBounds([[-133.2421875, 16.972741], [-47.63671875, 52.696361]]);
  // the rest of the code will go in here
            });    
        </script>
        

    </body>
</html>
