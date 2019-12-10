<template>
  <v-app>
    <div id="mapid"></div>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    //
  }),
  mounted() {
    var mymap = L.map("mapid").fitWorld();

    L.tileLayer(
      "https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}",
      {
        attribution:
          'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
        maxZoom: 18,
        id: "mapbox/streets-v11",
        accessToken:
          "pk.eyJ1IjoiZHBpZXJzYW50aSIsImEiOiJjazN6bXB0aGswNXgyM2xxdWI2aTJwcmdyIn0.jFXidtYiiYqIoyOPNNYquQ"
      }
    ).addTo(mymap);

    mymap.locate({ setView: true, maxZoom: 16 });

    function onLocationFound(e) {
      var radius = e.accuracy;

      L.marker(e.latlng).addTo(mymap);
      //.bindPopup("You are within " + radius + " meters from this point")
      //.openPopup();

      //L.circle(e.latlng, radius).addTo(mymap);
    }

    mymap.on("locationfound", onLocationFound);

    function onLocationError(e) {
      alert(e.message);
    }

    mymap.on("locationerror", onLocationError);
  }
};
</script>

<style>
#mapid {
  height: 500px;
}
</style>
