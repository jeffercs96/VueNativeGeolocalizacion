<template>
  <view>
    <view class="container">
      <text-input class="text-input" v-model="text" />
      <touchable-opacity class="button" :on-press="add">
        <text class="button-text">Agregar</text>
      </touchable-opacity>
      <touchable-opacity class="button" :on-press="clearList">
        <text class="button-text">Reset</text>
      </touchable-opacity>
    </view>
    <view class="test" v-for="(caracter, index) in listaCaracteres" :key="index">
      <touchable-opacity :on-press="() => remove(caracter)">
        <text class="text-container">{{ caracter }}</text>
      </touchable-opacity>
    </view>
  </view>
</template>

<script>
import { AsyncStorage } from "react-native";

export default {
  data() {
    return {
      text: "",
      listaCaracteres: []
    };
  },
  mounted() {
    this.get();
  },
  methods: {
    async add() {
      try {
        if (this.listaCaracteres.includes(this.text)) {
          alert("No puede ingresar lo mismo de nuevo");
        } else {
          await AsyncStorage.setItem(this.text, this.text);
          alert(this.text + " agregado!");
          this.listaCaracteres.push(this.text);
          console.log(this.listaCaracteres);
          this.text = "";
        }
      } catch (error) {
        console.log(error.message);
      }
    },
    async get() {
      try {
        const keys = await AsyncStorage.getAllKeys();
        // const items = await AsyncStorage.multiGet(keys);
        this.listaCaracteres = keys;
        // console.log(this.listaCaracteres);
      } catch (error) {
        console.log(error.message);
      }
    },
    async remove(caracter) {
      try {
        await AsyncStorage.removeItem(caracter);
        this.listaCaracteres = [];
        this.get();
      } catch (error) {
        console.log(error.message);
      }
    },
    async clearList() {
      try {
        await AsyncStorage.clear();
        this.listaCaracteres = [];
        alert("Datos borrados");
      } catch (error) {
        console.log(error.message);
      }
    }
  }
};
</script>

<style>
.container {
  background-color: #333;
  flex-direction: row;
  padding: 20px;
}
.test {
  align-items: center;
  justify-content: center;
  padding-top: 10;
}
.text-input {
  background-color: white;
  margin-right: 5px;
  flex: 3;
}
.text-container {
  color: black;
  padding: 2;
}
.button {
  flex: 1;
  background-color: #008080;
  margin-left: 5px;
  align-items: center;
  justify-content: center;
  padding-top: 10px;
  padding-bottom: 10px;
}
.button-text {
  color: white;
  font-weight: normal;
}
</style>
