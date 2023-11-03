<template>
    <div class="map-wrap">
        <div class="map" ref="mapContainer"></div>
    </div>
</template>

<script setup>
import { Map, MapStyle, Marker, config } from '@maptiler/sdk';
import { shallowRef, onMounted, onUnmounted, markRaw } from 'vue';
import '@maptiler/sdk/dist/maptiler-sdk.css';

const mapContainer = shallowRef(null);
const map = shallowRef(null);

onMounted(() => {
    config.apiKey = 'n09tiMVh0Ex76MEbIRfH';

    const initialState = { lng: 12.6392, lat: 5.6855, zoom: 50 };

    map.value = markRaw(new Map({
        container: mapContainer.value,
        style: MapStyle.STREETS,
        center: [initialState.lng, initialState.lat],
        zoom: initialState.zoom
    }));

    new Marker({ color: "#FF0000" })
        .setLngLat([12.6392, 5.6855])
        .addTo(map.value);

}),
    onUnmounted(() => {
        map.value?.remove();
    })
</script>

<style scoped>
.map-wrap {
    position: relative;
    width: 100%;
    height: calc(100vh - 77px);
    /* calculate height of the screen minus the heading */
}

.map {
    position: absolute;
    width: 100%;
    height: 100%;
}
</style>