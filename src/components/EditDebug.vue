<template>
    <textarea v-model="geojsonEdit"></textarea>
</template>

<script>
export default {
    name: 'EditDebug',
    props: {
        geojson: Object
    },
    computed: {
        geojsonEdit: {
            set(value) {
                // when the text is modified, a `change` event is emitted
                // note: we’re emitting an object from a string
                this.$emit('change', JSON.parse(value))
            },
            get() {
                // the text content is taken from the `geojson` prop
                // note: we’re getting a string from an object
                return JSON.stringify(this.geojson, null, ' ')
            }
        }
    },
    emits: ['change']
}
</script>

<style>
textarea {
    width: 100%;
    height: 100%;
    resize: none;
}
</style>