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



const x =ref('125')
const s = ref("80%")

const l_store = ref('50')
const l = ref('50%')
colourSelection.value = `hsl(${x.value}, ${s.value}, ${l.value})`

let fontColor = ref('black')
let setFontColor = ref('black')

function onMousemoveHue(e) {
    x.value = e.clientX
    colourSelection.value = `hsl(${x.value}, ${s.value}, ${l.value})`
}

function onMousemoveSat(e) {
    s.value = parseFloat(e.clientX/3.8).toFixed(0)+'%'
    colourSelection.value = `hsl(${x.value}, ${s.value}, ${l.value})`
}

function onMousemoveLum(e) {
    l_store.value = parseFloat(e.clientX/3.8).toFixed(0)
    if (l_store.value<50)
    {
        fontColor.value = 'white'
    }
    else {
        fontColor.value = 'black'
    }
    l.value = l_store.value+'%'
    colourSelection.value = `hsl(${x.value}, ${s.value}, ${l.value})`

}

function selectNavbar() {
    selector.value = "#navbar"
}

function selectMain() {
    selector.value = "#main"
}
function selectSidebar() {
    selector.value = "#sidebar"
}

function updateCSS() {
    if (l_store.value < 50) {
        setFontColor.value = 'white'
    }
    else {
        setFontColor.value = 'black'
    }
    const elements = document.querySelectorAll(selector.value)
    elements.forEach((element) => {
        //change the colour of the element
        element.style.background = colourSelection.value
        element.style.color = setFontColor.value
    })
}
</script>



<!-- the template is where the html code goes -->
<template>

<div id="navbar" class="container" @click="selectNavbar">
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
        
            
        <input type='text' v-model="colourSelection" placeholder="new background colour" />
        <button @click="updateCSS">Change background</button>
        <div
            @mousemove="onMousemoveHue"
            @click="updateCSS"
            class = "movearea">
            <p>hue {{ x }}</p>
        </div>
        <div
            @mousemove="onMousemoveSat"
            @click="updateCSS"
            class = "movearea">
            <p>saturation {{ s }}</p>
        </div>
        <div
            @mousemove="onMousemoveLum"
            @click="updateCSS"
            class = "movearea">
            <p>luminance {{ l }}</p>
        </div>
        <div @click="selectSidebar" class="expanding">
            <p><br></p>
        </div>
      </div>

      <div id="main" class="container" @click="selectMain">
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
  transition: 0.5s background-color ease;
  height: 23px;
  padding: 10px;
  border-radius: 1px;
  border-style: solid;
  display: flex;
  justify-content: center;
  align-items: center;
  border-color: grey;
  border-width: 1px;
  color: v-bind(fontColor);
  transition: 0.5s color ease;
}

.expanding {
    height: 100%;
}

</style>