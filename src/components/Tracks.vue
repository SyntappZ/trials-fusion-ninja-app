<template>
  <f7-block id="tracks">
    
      <f7-block v-for="track in tracks" :key="track.id">
        <f7-card class="card">
          <f7-card-header
            class="no-border"
            style="background-color:#038c73; color:white"
          >{{ track.trackName }}</f7-card-header>
          <f7-card-content>
            <f7-row>
              <p>{{ track.creator }}</p>
              <p></p>
          
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
      tracks: trackList.reverse(),
      color: "pink"
    };
  },
  methods: {
    searchTracks(name, creator, level, fwBw) {
      this.tracks = trackList;
      if (name === "") {
        this.tracks = this.tracks;
      } else {
        this.tracks = this.tracks.filter(
          track => track.trackName.toLowerCase() == name.toLowerCase()
        );
      }
      if (creator === "") {
        this.tracks = this.tracks;
      } else {
        this.tracks = this.tracks.filter(
          track => track.creator.toLowerCase() == creator.toLowerCase()
        );
      }
      if (level === "All") {
        this.tracks = this.tracks;
      } else {
        this.tracks = this.tracks.filter(track => track.level == level);
      }
      if (fwBw === "both") {
        this.tracks = this.tracks;
      } else {
        this.tracks = this.tracks.filter(track => track.fwBw == fwBw);
      }
    }
  },
  computed: {
    sortTracks() {}
  }
};
</script>
<style scoped>
#tracks {
  width: 100%;
  margin: 0;
  padding: 0;
}
</style>


