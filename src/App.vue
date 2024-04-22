<template>
  <div id="app">
    <div class="toolbar">
      <MultiSelectRegion v-on:change="geojson = $event">
      </MultiSelectRegion>
    </div>
    <div class="cell-container">
      <div class="cell cell-map">
        <MapContainer :geojson="geojson" v-on:select="selected = $event"></MapContainer>
      </div>
      <div class="cell cell-debug">
        <div class="cell cell-edit">
          <EditDebug :geojson="geojson" v-on:change="geojson = $event">
          </EditDebug>
        </div>
        <div class="cell cell-inspect">
          <InspectDebug :feature="selected">
          </InspectDebug>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import MapContainer from "./components/MapContainer.vue";
import EditDebug from "./components/EditDebug.vue";
import InspectDebug from "./components/InspectDebug.vue";
import MultiSelectRegion from "./components/MultiSelectRegion.vue";

export default {
  name: 'App',
  components: {
    MapContainer,
    EditDebug,
    InspectDebug,
    MultiSelectRegion
  }, data: () => ({
    regions: undefined,
    selected: undefined,
    // this is the initial GeoJSON data
    geojson: {
      type: 'Feature',
      properties: {},
      geometry: {
        type: 'Polygon',
        coordinates: [
          [
            [
              -27.0703125,
              43.58039085560784
            ],
            [
              -28.125,
              23.563987128451217
            ],
            [
              -10.8984375,
              32.84267363195431
            ],
            [
              -27.0703125,
              43.58039085560784
            ]
          ]
        ]
      }
    }
  })
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
  flex-direction: column;
  padding: 1rem;
  box-sizing: border-box;
}

.cell {
  border-radius: 4px;
  background-color: lightgrey;
}

.cell-container {
  flex: 10;
  display: flex;
  flex-direction: row;
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

.toolbar {
  flex: 1;
  display: flex;
}
</style>
