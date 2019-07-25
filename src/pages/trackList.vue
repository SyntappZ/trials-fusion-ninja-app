<template>
  <f7-page id="tracklist">
   

    <f7-navbar back-link="Back">
      <f7-nav-title>track list</f7-nav-title>
      <f7-nav-right>
        <f7-link popup-open=".popup">Search</f7-link>
      </f7-nav-right>
    </f7-navbar>

    <tracks ref="search"/>
    <f7-popup class="popup" :opened="popupOpened" @popup:closed="popupOpened = false">
      <f7-page>
        <f7-navbar title="Search Tracks">
          <f7-nav-right>
            <f7-link popup-close>Close</f7-link>
          </f7-nav-right>
        </f7-navbar>

        <f7-block>
          <f7-list no-hairlines-md>
            <f7-list-input
              @input="trackName = $event.target.value"
              outline
              label="Track Name"
              floating-label
              type="text"
              clear-button
            ></f7-list-input>
            <f7-list-input
              @input="creator = $event.target.value"
              outline
              label="Creator"
              floating-label
              type="text"
              clear-button
            ></f7-list-input>
            <f7-list-input defaultValue="All"  @input="ninjaLevel = $event.target.value" label="Ninja Level" type="select">
              <option value="null">All</option>
              <option value="1">ninja Level 1</option>
              <option value="2">Ninja Level 2</option>
              <option value="3">Ninja Level 3</option>
              <option value="4">Ninja Level 4</option>
              <option value="5">Ninja Level 5</option>
              <option value="6">Ninja Level 6</option>
              <option value="7">Ninja Level 7</option>
              <option value="8">Ninja Level 8</option>
            </f7-list-input>
          </f7-list>
          <f7-block-title>FW/BW</f7-block-title>
          <f7-list no-hairlines-md>
            <f7-list-item
              :checked="fwBw === 'both'"
              @change="fwBw = $event.target.value"
              radio
              title="BOTH"
              name="fwbw"
               value="both"
            ></f7-list-item>
            <f7-list-item
              :checked="fwBw === 'fwbw'"
              @change="fwBw = $event.target.value"
              radio
              title="FW/BW ONLY"
              name="fwbw"
               value="Yes"
            ></f7-list-item>
            <f7-list-item
              :checked="fwBw === 'noFwbw'"
              @change="fwBw = $event.target.value"
              radio
              title="NO FW/BW"
              name="fwbw"
               value="No"
            ></f7-list-item>
          </f7-list>
          <f7-button popup-close @click="GetSearchDetails">Search</f7-button>
        </f7-block>
      </f7-page>
    </f7-popup>
  </f7-page>
</template>

<script>
import tracks from "../components/Tracks";

import TrackList from "../js/trialsTracks.js";
export default {
  components: {
   
    tracks
  },

  data() {
    return {
      trackList: TrackList,
      popupOpened: false,
      trackName: "",
      creator: "",
      ninjaLevel: 'All',
      fwBw: 'both',
    
    };
  },
  methods: {
    GetSearchDetails() {
      this.$refs.search.searchTracks(this.trackName, this.creator, this.ninjaLevel, this.fwBw);
     
    }
    
  }
};
</script>

<style scoped>
</style>

