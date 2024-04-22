<template>
    <div ref="map-root" style="width: 100%; height: 100%">
    </div>
</template>

<script>
import View from 'ol/View'
import Map from 'ol/Map'
/*
import TileLayer from 'ol/layer/Tile'
import OSM from 'ol/source/OSM'*/

// importing the OpenLayers stylesheet is required for having
// good looking buttons!
import 'ol/ol.css'
import VectorSource from 'ol/source/Vector'
import VectorLayer from 'ol/layer/Vector'
import GeoJSON from 'ol/format/GeoJSON'

export default {
    name: 'MapContainer',
    components: {},
    props: {
        geojson: Object
    },
    data: () => ({
        // store OL objects on the component instance
        olMap: null,
        vectorLayer: null
    }),
    mounted() {

        // a new vector layer is created with the feature
        this.vectorLayer = new VectorLayer({
            source: new VectorSource({
                features: [],
            }),
        })
        // this is where we create the OpenLayers map
        this.olMap = new Map({
            // the map will be created using the 'map-root' ref
            target: this.$refs['map-root'],
            layers: [
                /*
                // adding a background tiled layer
                new TileLayer({
                    source: new OSM() // tiles are served by OpenStreetMap
                }),*/
                // the vector layer is added above the tiled OSM layer
                this.vectorLayer
            ],

            // the map view will initially show the whole world
            view: new View({
                zoom: 0,
                center: [0, 0],
                constrainResolution: true
            }),
        })
        this.olMap.on('pointermove', (event) => {
            // will return the first feature under the pointer
            const hovered = this.olMap.forEachFeatureAtPixel(
                event.pixel,
                (feature) => feature
            )

            // emit a `select` event, either with a feature or without
            this.$emit('select', hovered)
        })

        // we’re calling `updateSource` to show the object initially
        this.updateSource(this.geojson)
    },
    watch: {
        geojson(value) {
            // call `updateSource` whenever the input changes as well
            this.updateSource(value);
        }
    },
    methods: {
        // this will parse the input data and add it to the map
        updateSource(geojson) {
            const view = this.olMap.getView();
            const source = this.vectorLayer.getSource();
            const features = new GeoJSON({
                featureProjection: 'EPSG:3857',
            }).readFeatures(geojson)

            source.clear();
            source.addFeatures(features);

            // this zooms the view on the created object
            view.fit(source.getExtent());
        }
    },
    emits: ['select']
}
</script>