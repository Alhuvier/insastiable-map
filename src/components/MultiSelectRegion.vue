<template>
    <div>
        <select v-model="regions" @change="changeRegion($event)">
            <option v-for="option in options" :key="option.value">
                {{ option.text }}
            </option>
        </select>
        <div>Selected: {{ regions }}</div>
    </div>
</template>

<script>
export const regionsAPI = {
    Bretagne: "bretagne",
    Normandie: "normandie",
    "Pays de la Loire": "pays-de-la-loire",
    "Hauts de France": "hauts-de-france"
};
let regionsToShow = [
    { text: 'Bretagne', value: 'bretagne' },
    { text: 'Normandie', value: 'normandie' },
    { text: 'Pays de la Loire', value: 'pays-de-la-loire' },
    { text: 'Hauts de France', value: 'hauts-de-france' }
]
export default {
    name: 'MultiSelectRegion',
    data() {
        return {
            regions: [regionsToShow[0].text],
            options: regionsToShow
        }
    },
    methods: {
        changeRegion() {
            let regions = regionsAPI[this.regions];
            let url = `https://france-geojson.gregoiredavid.fr/repo/regions/${regions}/region-${regions}.geojson`;
            fetch(url)
                .then((response) => response.json())
                .then((json) => {
                    console.log(json)
                    this.$emit('change', json);
                }).catch((e) => {
                    console.error(e);
                })
        }
    },
    emits: ['change']
}

</script>

<style></style>