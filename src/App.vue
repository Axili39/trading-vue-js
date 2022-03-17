<template>
    <trading-vue
        :data="chart"
        :width="width"
        :height="height"
        :color-back="colors.colorBack"
        :color-grid="colors.colorGrid"
        :color-text="colors.colorText"
    ></trading-vue>
</template>

<script setup>
import { reactive, onMounted, computed } from 'vue'
import TradingVue from './TradingVue.vue'
import Data from '../data/data.json'
import DataCube from '../src/helpers/datacube.js'

const chart = ref(new DataCube(Data))
const width = ref(window.innerWidth)
const height = ref(window.innerHeight)
const colors = ref({
    colorBack: '#fff',
    colorGrid: '#eee',
    colorText: '#333',
})

onMounted(() => {
    window.addEventListener('resize', onResize)
    window.dc = this.chart
})

beforeUnmount(() => {
    window.removeEventListener('resize', onResize)
})

onResize(() => {
    width.value = window.innerWidth
    height.value = window.innerHeight
})

</script>

<style>
html,
body {
    background-color: #000;
    margin: 0;
    padding: 0;
    overflow: hidden;
}
</style>
