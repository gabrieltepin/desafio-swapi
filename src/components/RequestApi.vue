<template>
    <div>
        <br>
        <p v-if = "notClicked">
            <button @click="loadJson" class="button">Creditos</button>
        </p>
        <div>
            <br>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data(){
        return{
            notClicked: false,
            myjson: '',
            url:'https://swapi.co/api/people/',
            //link for testing purposes
            //url: 'http://ron-swanson-quotes.herokuapp.com/v2/quotes' 
            persons: [],
            eyeColors: [],
        }
    },
    created(){
        this.loadJson();
    },
    methods: {
        dynamicSort(property) {
            var sortOrder = 1;
            //if some wish to display reversed order
            if(property[0] === "-") {
                sortOrder = -1;
                property = property.substr(1);
            }
            return function (a,b) {
                var result = (a[property] < b[property]) ? -1 : (a[property] > b[property]) ? 1 : 0;
                return result * sortOrder;
            }
        },
        loadJson(){
            var vm = this;
            vm.notClicked=!vm.notClicked;
            axios
                .get(vm.url)
                .then(function(response){
                    vm.myjson = response.data
                })
                .catch(function(error){
                    vm.myjson = 'error: ' + error;
                })
            vm.myjson.results.sort(vm.dynamicSort("name"));
            vm.$emit('jsonReceived', vm.myjson);
            
            //other properties transmited to parent component in case we would like to use them
            vm.persons=[];
            for(var obj in vm.myjson.results){
                var myobj;
                myobj.name = vm.myjson.results.name;
                myobj.eye_color = vm.myjson.results.eye_color;
                vm.persons.push(myobj);
            }
            vm.persons.sort();
            vm.$emit('personArray', vm.persons);
            vm.$emit('eyeColorsArray', vm.eyeColors);
        }
    },
}
</script>

<style scoped>
.button{
    color: #494949 !important;
    text-transform: uppercase;
    text-decoration: none;
    background: #ffffff;
    padding: 20px;
    border: 4px solid #494949 !important;
    display: inline-block;
    transition: all 0.4s ease 0s;
}
</style>