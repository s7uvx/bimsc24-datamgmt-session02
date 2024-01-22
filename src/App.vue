<!-- the script is where the js code goes -->
<script setup>

import { ref } from "vue"

// Define variables and constants

const newText = ref('')
let outputText = ref('')

let selector = ref('#title')
let colourSelection = ref('')


function updateText() {

    outputText.value += newText.value
    outputText.value += '\n'
    newText.value = ""
}

function clearText() {

    outputText.value = ""

}

function updateCSS() {
    const elements = document.querySelectorAll(selector.value)
    elements.forEach((element) => {
        //change the colour of the element
        element.style.background = colourSelection.value
    })
}

const x =ref(0)
const s = ref("80%")
const l = ref("50%") 

function onMousemove(e) {
    x.value = e.clientX
    colourSelection.value = `hsl(${x.value}, ${s.value}, 50%)`
}

function setToNavbar() {
    selector.value = "#navbar"
}

function setToMain() {
    selector.value = "#main"
}

</script>



<!-- the template is where the html code goes -->
<template>

<div id="navbar" class="container" @click="setToNavbar">
      <div id="title">It's a cow!</div>
      <div id="logo">
        <img src="\src\assets\cow.jpg" alt="macad cow" />
      </div>
    </div>

    <div id="flex">
      <div id="sidebar" class="container">
        <input type='text' v-model="newText" placeholder="Add Text" v-on:keyup.enter="updateText"/>
        <button @click="updateText"> Add text </button>
        <button @click="clearText"> Clear text</button>
        <p><br></p>
        <input type='text' v-model="selector" placeholder="element type" />
        <div
            @mousemove="onMousemove"
            @click="updateCSS"
            class = "movearea">
        <p>Click to set colour</p>
        </div>
            
        <input type='text' v-model="colourSelection" placeholder="new background colour" />
        <button @click="updateCSS">Change background</button>
      </div>

      <div id="main" class="container" @click="setToMain">
        <!-- <p> input text is {{ newText }} </p> -->
        <p class="newlineStringStyle"> <pre>{{ outputText }}</pre> </p>

      </div>
    </div>


</template>



<!-- style is where the css code goes -->
<style scoped>
html{
    
    background: -webkit-linear-gradient(270deg, rgba(0,0,0,1.0), #21D4FD 50%); 
    color: white;
}

body{

    margin:0;
}

div{

    /* put the borders in the inside of container */
    box-sizing: border-box;
}

img{

    height: 100%;
    width: auto;

}

input{
    width: 90%;
}


#navbar{

    height: 100px;
    border-color: red;


}

#flex{
    
    display: flex;
    height: calc(100vh - 50px);
}

#sidebar{
    
    width:20%;
    border-color: blue;

}

#main{
    width:80%;
    border-color: green;

}

#title{
    width: 70%;
    float:left;
    font-size: 80px;
}

#logo{
    width: 30%;
    height: 100%;
    float:right;
    text-align: right;

}

.container{

    border-style: dotted;
    border-width: 1px;
    

}

.newlineStringStyel {
    white-space: pre-wrap;
}

.movearea {
  background-color: v-bind(colourSelection);
  transition: 0.3s background-color ease;
  height: 50px;
  padding: 10px;
  border-radius: 3px;
  display: flex;
  justify-content: center;
  align-items: center;
}

</style>