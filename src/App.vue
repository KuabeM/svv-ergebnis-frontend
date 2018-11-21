<template>
  <div id="app">
    <Headline/>
    <Competitors value="[SV Vötting Weihenstephan, BSG Taufkirchen]"/>
    <!-- <Score value="0"/> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Headline from './components/Headline.vue'
// import Score from './components/Score.vue'
import Competitors from './components/Competitors.vue'

export default {
  name: 'app',
  components: {
    // HelloWorld,
    Headline,
    Competitors,
    // Score,
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
  padding: 0;
}


body {
  margin:0;
}

input[type='number'] {
    -moz-appearance:textfield;
} input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    -webkit-appearance: none;
}

button {
    display: inline-block;
    font-weight: 400;
    text-align: center;
    white-space: nowrap;
    vertical-align: middle;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    border: 1px solid transparent;
    padding: .375rem .75rem;
    font-size: 1rem;
    line-height: 1.5;
    border-radius: .25rem;
    color: #fff;
    background-color: #28a745;
    border-color: #28a745;
    cursor: pointer;
    text-transform: none;
    transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
}

button:hover {
    color: #fff;
    background-color: #218838;
    border-color: #1e7e34;
}

</style>
