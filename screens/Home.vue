<template>
  <view class="container">
    <view class="statusbar" />

    <view class="efe">
      <image class="test" :source="{ uri: imagen }" />
      <button title="Foto" @press="tomarFoto"></button>
    </view>

    <view class="efe">
      <video class="test" :source="{ uri: video }" useNativeControls resizeMode="contain" />
      <button title="Video" @press="tomarVideo"></button>
    </view>
  </view>
</template>

<script>
import { Video } from "expo-av";
export default {
  data() {
    return {
      imagen:
        "https://picsum.photos/id/11/500/300",
      video:
        "http://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4"
    };
  },
  props: {
    navigation: {
      type: Object
    }
  },
  methods: {
    tomarFoto() {
      this.navigation.navigate("Camara", {
        onGoBack: this.refresh,
        tipo: "Foto"
      });
    },
    tomarVideo() {
      this.navigation.navigate("Camara", {
        onGoBack: this.refresh,
        tipo: "Video"
      });
    },
    refresh(data, tipo) {
      tipo == "Foto" ? (this.imagen = data) : (this.video = data);
    }
  },
  components: { Video }
};
</script>

<style>
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: white ;
}
.statusbar {
  background-color: black;
  /* height: 110; */
  height: 20;
}
.efe {
  padding: 10;
  margin: 10;
}
.test {
  width: 325;
  height: 200;
  border-color: black;
  border-width: 1;
}
</style>
