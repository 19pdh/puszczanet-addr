<template>
  <div id="app">
    <vl-map :load-tiles-while-animating="true" :load-tiles-while-interacting="true"
             data-projection="EPSG:4326" style="height: 50vh" @click="getLoction"
             class="map">
      <vl-view :zoom.sync="zoom" :center.sync="center" :rotation.sync="rotation"></vl-view>

      <vl-layer-tile id="osm">
        <vl-source-osm></vl-source-osm>
      </vl-layer-tile>
    </vl-map>
    <div id="qr">
      <qr-code v-if="show" :cords="cords"/>
      <input type="text" v-model="cords" v-if="show">
      <p v-if="!show">Kliknij lokalizację na mapie...</p>
    </div>
  </div>
</template>

<script>
import QRCode from './components/QRCode.vue';

  export default {
  components: { "qr-code": QRCode },
    data () {
      return {
        zoom: 10,
        center: [16.93, 52.41],
        rotation: 0,
        cords: "",
        show: false
      }
    },
    methods: {
      getLoction(e) {
        this.cords = `(${e.coordinate[1]}, ${e.coordinate[0]})`;
        console.log(this.cords);
        this.show = true;
      }
    }
  }
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
}

.map {
  cursor: pointer;
}

#qr {
  height: 50vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

input {
  text-align: center;
  width: 80%;
  max-width: 300px;
  margin: 1px;
  border: none;
}
</style>
