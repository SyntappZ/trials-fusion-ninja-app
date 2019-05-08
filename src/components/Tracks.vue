<template>
  <f7-block id="jeff">
    <f7-block-title color="primary" medium>Fusion Ninja Tracks</f7-block-title>
    <f7-button @click="test">press</f7-button>

    <f7-block v-for="track in tracks" :key="track.id">
      <f7-card class="demo-card-header-pic">
        <f7-card-header
          class="no-border"
          style="background-color:#038c73; color:white"
        >{{ track.trackName }}</f7-card-header>
        <f7-card-content>
          <f7-row>
            <p>{{ track.creator }}</p>
            <f7-icon style="color:#038c73" v7="heart_fill"></f7-icon>
          </f7-row>
        </f7-card-content>
        <f7-card-footer>
          <h3 style="color:${ color }">N{{ track.level }}</h3>
          <div>
            <span>FW BW</span>
            <f7-icon v-if="track.fwBw === 'Yes'" style="color:#038c73" f7="tick">check</f7-icon>
            <f7-icon v-else style="color:red" f7="tick">close</f7-icon>
          </div>
        </f7-card-footer>
      </f7-card>
    </f7-block>
  </f7-block>
</template>

<script>
import trackList from "../js/trialsTracks.js";
export default {

  created() {},
  data() {
    return {
      tracks: trackList,
      trackName: "Main Drain",
      creator: "JamaicanX",
      ninjaLevel: "N4",
      fwBw: "yes",
      color: "pink"
    };
  },
  methods: {
    test(info) {
    
     let ftracks = this.tracks.filter(track => track.level == info.ninjaLevel)
  this.tracks = ftracks;
    }

  },
  computed: {
  
  }
};
</script>
<style scoped>
</style>


function newFunction() {
  return '2';
}
