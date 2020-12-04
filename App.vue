<template>
  <app-navigator></app-navigator>
</template>

<script>
import {
  createAppContainer,
  createMaterialTopTabNavigator,
  createBottomTabNavigator,
  createStackNavigator
} from "vue-native-router";

import CameraScreen from "./screens/Camera.vue";
import HomeScreen from "./screens/Home.vue";
import WebServiceScreen from "./screens/WebService.vue";
import DatabaseScreen from "./screens/Database.vue";
//import ImageBrowserScreen from "./screens/ImageBrowser.vue";
import GeolocationScreen from "./screens/Geolocation.vue";


const Tabs = createMaterialTopTabNavigator({
  Camera: HomeScreen,
  API: WebServiceScreen,
  DB: DatabaseScreen,
  // API2: ImageBrowserScreen,
  Map: GeolocationScreen,
});

const StackNavigator = createStackNavigator(
  {
    Tabs,
    Camara: CameraScreen
  },
  {
    defaultNavigationOptions: {
      gestureEnabled: false,
      title: "Fotos & Video",
      headerTitleStyle: {
        textAlign: "center",
        alignSelf: "center",
        color: "white"
      },
      headerStyle: {
        backgroundColor: "black"
      }
    }
  }
);

const AppNavigator = createAppContainer(StackNavigator);

export default {
  components: { AppNavigator }
};
</script>
