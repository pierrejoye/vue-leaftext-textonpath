<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <div id="map"></div>
  </div>
</template>

<script>
import L from 'leaflet';
import 'leaflet-textpath';
console.log(L);
export default {
  name: "Hello Leaf",
  props: {
    msg: String,
  },

  mounted() {
    //const L = require("leaflet-textpath");
    console.log(L);
    var osm = L.tileLayer("//{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
      attribution: "Map data &copy; 2013 OpenStreetMap contributors",
    });

    var map = L.map("map").fitWorld().addLayer(osm);

    var wind = L.polyline(
      [
        [59.3556, -31.99219],
        [55.17887, -42.89062],
        [47.7541, -43.94531],
        [38.27269, -37.96875],
        [27.05913, -41.13281],
        [16.29905, -36.5625],
        [8.40717, -30.23437],
        [1.05463, -22.5],
        [-8.75479, -18.28125],
        [-21.61658, -20.03906],
        [-31.35364, -24.25781],
        [-39.90974, -30.9375],
        [-43.83453, -41.13281],
        [-47.7541, -49.92187],
        [-50.95843, -54.14062],
        [-55.9738, -56.60156],
      ],
      {
        weight: 15,
        color: "#8EE9FF",
      }
    ).addTo(map);
    wind.setText(") ", {
      repeat: true,
      offset: 7,
      attributes: { fill: "#007DEF", "font-weight": "bold", "font-size": "24" },
    });

    var danger = L.polyline(
      [
        [-40.311, -31.952],
        [-12.086, -18.727],
      ],
      {
        weight: 10,
        color: "orange",
        opacity: 0.8,
      }
    ).addTo(map);
    danger.setText("\u25BA", {
      repeat: true,
      offset: 6,
      attributes: { fill: "red" },
    });

    var plane = L.polyline(
      [
        [-49.38237, -37.26562],
        [-1.75754, -14.41406],
        [51.61802, -23.20312],
      ],
      {
        weight: 1,
        color: "black",
        dashArray: "2, 2",
      }
    ).addTo(map);
    plane.setText("\u2708     ", {
      repeat: true,
      offset: 8,
      attributes: { "font-weight": "bold", "font-size": "24" },
    });

    var flightsWE = {
      type: "FeatureCollection",
      features: [
        {
          type: "Feature",
          properties: {
            flight: "To New Delhi",
          },
          geometry: {
            type: "LineString",
            coordinates: [
              [3.33984375, 46.6795944656402],
              [29.53125, 46.55886030311719],
              [51.328125, 42.293564192170095],
              [68.5546875, 35.746512259918504],
              [76.81640625, 28.65203063036226],
            ],
          },
        },
        {
          type: "Feature",
          properties: {
            flight: "To Hanoi",
          },
          geometry: {
            type: "LineString",
            coordinates: [
              [77.607421875, 28.767659105691255],
              [88.72558593749999, 27.839076094777816],
              [97.3828125, 25.681137335685307],
              [105.77636718749999, 21.248422235627014],
            ],
          },
        },
      ],
    };

    var flightsEW = {
      type: "FeatureCollection",
      features: [
        {
          type: "Feature",
          properties: {
            flight: "To Bangkok",
          },
          geometry: {
            type: "LineString",
            coordinates: [
              [106.67724609375, 10.790140750321738],
              [104.08447265624999, 11.523087506868514],
              [102.1728515625, 12.254127737657381],
              [100.45898437499999, 13.667338259654947],
            ],
          },
        },
      ],
    };

    L.geoJson(flightsWE, {
      onEachFeature: function (feature, layer) {
        layer.setText(feature.properties.flight, { offset: -5 });
      },
      style: {
        weight: 3,
        color: "purple",
        dashArray: "4, 4",
      },
    }).addTo(map);

    L.geoJson(flightsEW, {
      onEachFeature: function (feature, layer) {
        layer.setText(feature.properties.flight, {
          offset: -5,
          orientation: "flip",
        });
      },
      style: {
        weight: 3,
        color: "purple",
        dashArray: "4, 4",
      },
    }).addTo(map);

    var pos1 = [40.418075, -3.704643],
      pos2 = [40.413119, -3.702369];
    var line = L.polyline([pos1, pos2]);
    line.setText("HOLA", { center: true, attributes: { fill: "red" } });
    line.addTo(map);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
