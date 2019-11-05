<template>
  <div id="app">
    <!-- Comunication of properties between sibling components -->
    <request-api 
      @jsonReceived = "myJson = $event" 
      @personArray = "myPersonArray = $event" 
      @eyeColorsArray = "myEyeColorsArray=$event">
    </request-api>
    <br>
    <personagem 
      :myJson="myJson" 
      :myPersonArray="myPersonArray" 
      :myEyeColorsArray="myEyeColorsArray">
    </personagem>
  </div>
</template>

<script>
import RequestApi from  './components/RequestApi.vue';
import Personagem from './components/Personagem.vue';
import axios from 'axios';
export default {
  components: {
    'request-api': RequestApi,
    'personagem': Personagem,
  },
  data () {
    return {
      myJson: '',
      myPersonArray: '',
      myEyeColorsArray: ''
    }
  },
  methods: {
    
  },
}
</script>

<style scooped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body {
  margin: 0;
  background-color: black;
}
</style>
