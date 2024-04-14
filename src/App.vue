<template>
  <div id="app">
    <div class="cell cell-map">
      <MapContainer />
    </div>
    <div class="cell cell-debug">
      <div class="cell cell-edit">
        Edit
      </div>
      <div class="cell cell-inspect">
        Inspect
      </div>
    </div>
  </div>
</template>

<script>
import MapContainer from "./components/MapContainer.vue";
export default {
  name: 'App',
  components: {
    MapContainer
  }
}
</script>

<style>
html,
body {
  height: 100%;
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  height: 100%;
  display: grid;
  display: flex;
  flex-direction: row;
  padding: 1rem;
  box-sizing: border-box;
}

.cell {
  border-radius: 4px;
  background-color: lightgrey;
}

.cell-map {
  flex: 2
}

.cell-debug {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.cell-edit {
  flex: 1;
  display: flex;
}

.cell-inspect {
  flex: 1;
  display: flex;
}
</style>
