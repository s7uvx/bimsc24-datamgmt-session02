<!-- the script is where the js code goes -->
<script setup>

import { ref } from "vue"

// Define variables and constants

const newText = ref('')
let outputText = ref('')

let selector = ref('')
let colorSelection = ref('')


function updateText() {

    outputText.value += newText.value
    outputText.value += '\n'
}

// function updateColors() {


// }

</script>



<!-- the template is where the html code goes -->
<template>

<div id="navbar" class="container">
      <div id="title">It's a cow!</div>
      <div id="logo">
        <img src="\src\assets\cow.jpg" alt="macad cow" />
      </div>
    </div>

    <div id="flex">
      <div id="sidebar" class="container">
        <input type='text' v-model="newText" placeholder="Text" />
        <button @click="updateText"> Add text </button>
        <!-- <p>{{ outputText }}</p> -->
      </div>

      <div id="main" class="container">
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

#navbar{

    height: 100px;
    border-color: red;


}

#flex{
    
    display: flex;
    height: calc(100vh - 50px);
}

#sidebar{
    
    width:30%;
    border-color: blue;

}

#main{
    width:70%;
    border-color: green;

}

#title{
    width: 70%;
    float:left;
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
    color: v-bind('colorSelection')

}

.newlineStringStyel {
    white-space: pre-wrap;
}

</style>