<template>
  <div>
      <span class="yellow"> {{myPersonArray}} </span>
      <div>
        <section class="intro">
            A long time ago, in a galaxy far,<br> far away....
        </section>
        <section class="logo">
            <img src="https://upload.wikimedia.org/wikipedia/commons/9/9b/Star_Wars_Yellow_Logo.svg">
        </section>
            <div id="board">  
                <div id="content">
                    <p id="title">DESCOMPLICA</p>
                    <p id="subtitle">O RETORNO DE TEODORO</p>
                    <br>
                    <button @click = "removePerson($index)" class="button">Eject</button>
                    <!-- exhibiting the star wars generated persons form the SWAPI API -->
                    <div>
                        <div v-for = "(obj, n, index) in myJson.results"> 
                            <span :style = "{color:obj.eye_color}"> {{obj.name}}</span>  
                            <!-- if you want to select the person to exclude, just uncomment the line below-->
                            <!-- <button @click = "removePerson($event, index)" class="button">Eject</button> -->
                        </div>
                    </div>
                </div>  
            </div>
        </div>
  </div>
</template>

<script>
    export default{
        //properties to comunicate between components
        props:{
            myJson: Object,
            myPersonArray: Array,
            myEyeColorsArray: Array
        },
        data(){
            return{
                index: 0
            }
        },
        methods:{
            removePerson(index) {
                var vm = this;
                vm.index = index;
                vm.myJson.results.splice(vm.index, 1)
            }
        }
    }
</script>

<style scoped>
.arr{
    color: yellow;
}
.star {
  position: absolute;
  width: 1px;
  height: 1px;
  background-color: white;
}
.intro {
    position: absolute;
    top: 45%;
    left: 50%;
    z-index: 1;
    animation: intro 6s ease-out 1s;
    color: rgb(75, 213, 238);
    font-weight: 400;
    font-size: 300%;
    opacity: 0;
}

@keyframes intro {
    0% {
        opacity: 0;
    }
    20% {
        opacity: 1;
    }
    90% {
        opacity: 1;
    }
    100% {
        opacity: 0;
    }
}
.logo {    
    position: absolute;
    top: 20%;
    left: 5%;
    z-index: 1;
    margin: auto;
    animation: logo 3s ease-out 7s;
    opacity: 0;
}

.logo svg {
    width: inherit;
}

/* Scale the logo down and maintain it centered */
@keyframes logo {
    0% {
        width: 18em;        
        transform: scale(2.75);
        opacity: 1;
    }
    50% {
        opacity: 1;
        width: 18em;      
    }
    100% {
        opacity: 0;
        transform: scale(0.1);
        width: 18em;        
   }
}
p {
  color: #FFFF82;
}

/* Set the font, lean the board, position it */
#board {
  font-family: Century Gothic, CenturyGothic, AppleGothic, sans-serif;
  transform: perspective(300px) rotateX(25deg);
  transform-origin: 50% 100%;
  text-align: justify;
  position: absolute;
  margin-left: -9em;
  font-weight: bold;
  overflow: hidden;
  font-size: 350%;
  height: 50em;
  width: 18em;
  bottom: 0;
  left: 50%;
}

#board:after {
  position: absolute;
  content: ' ';
  bottom: 60%;
  left: 0;
  right: 0;
  top: 0;
}

/* Set the scrolling animation and position it */
#content {
  animation: scroll 100s linear 8s;
  position: absolute;
  top: 100%;
}

#title, #subtitle {
  text-align: center;
}

@keyframes scroll {
    0% {
        top: 100%;
    }
    100% {
        top: -170%;
    }
}
</style>
