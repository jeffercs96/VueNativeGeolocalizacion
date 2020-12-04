<template>
  <view class="container">
    <text class="coordena">Coordenada Actual</text>
    <text>Latitud: {{ coordinates.latitude }}</text>
    <text>Longitud: {{ coordinates.longitude }}</text>
    
    <MapView class="mapa" :initial-region="coordinates" :onRegionChange="onRegionChange" ref="mapa">
      <Marker
        title="Tu localización"
        :coordinate="{
          latitude: coordinates.latitude,
          longitude: coordinates.longitude
          }"
        draggable
      />
    </MapView>
    
    <touchable-opacity>
      <button title="Obtener mis coordenadas" @press="getLocation"></button>
    </touchable-opacity>
  </view>
</template>

<script>
import * as Permissions from "expo-permissions";
import * as Location from "expo-location";
import MapView, { Marker } from "react-native-maps";

import axios from "axios";

export default {
  data() {
    return {
      errorMessage: "",
      coordinates: {
        latitude: -0.167423,
        longitude: -78.472858,
        latitudeDelta: 0.0001,
        longitudeDelta: 0.01
      },
      apiKey: "802371203359246534665x6018",
      locationText: ""
    };
  },
  mounted() {},
  methods: {
    getLocation() {
      Permissions.askAsync(Permissions.LOCATION)
        .then(status => {
          if (status !== "granted") {
            this.errorMessage = "Permission to access location was denied";
          }

          Location.getCurrentPositionAsync({}).then(location => {
            // this.coordinates.latitude = location.coords.latitude;
            // this.coordinates.longitude = location.coords.longitude;
            console.log(this.coordinates);
            this.$refs.mapa.animateToRegion(
              {
                latitude: location.coords.latitude,
                longitude: location.coords.longitude,
                latitudeDelta: 0.0001,
                longitudeDelta: 0.01
              },
              10
            );
            // console.log(this.location.coords.latitude);
          });
        })
        .catch(err => {
          console.log(err);
        });
    },
    onRegionChange(region) {
      this.coordinates = region;
    },
  },
  components: { MapView, Marker }
};
</script>

<style>
.container {
  flex: 1;
  background-color: white;
  align-items: center;
  justify-content: center;
}
.mapa {
  height: 500px;
  width: 400px;
}
.text-color-primary {
  color: blue;
}
</style>
