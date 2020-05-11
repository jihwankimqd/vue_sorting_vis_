<template>
  <div id="app">
    <vue-sorting></vue-sorting>
  </div>
</template>

<script>

import vuequicksort from './components/vue-sorting';

export default {
  name: 'App',
  components: {
    'vue-sorting':vuequicksort,
  }
}
</script>

<style>
.container {
  position: absolute;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  background-color:white;
  display: flex;
  align-items: flex-end;
}

.item {
  background-color: lightgreen;
  border: solid 0.5px rgb(25, 190, 25);
}

.item.in-range {
  background-color: #7C7C7C;
}

.control_delay{
  color: black
}

.controls {
  font-family: "Gill Sans", sans-serif;
  position: absolute;
  top: 0;
  right: 0;
  margin: 1em;
  background-color:greenyellow;
  padding: 10px;
}
.controls input[type="number"] {
  line-height: 2em;
  border: none;
  margin: 2px 0px;
  width: 50px
}
.btn {
  margin-left: 10px;
}
.btn-sort {
  padding: 5px 10px;
  font-size: 1em;
  background-color:rgb(25, 190, 25);
  border: none;
  outline: none;
  color: black;
  cursor: pointer;
  float: right;
}
.btn-sort:active {
  background-color: #F9DC5C;
  color: black;
}
</style>
