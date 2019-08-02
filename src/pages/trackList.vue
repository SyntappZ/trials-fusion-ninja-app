<template>
  <f7-page id="tracklist">
    <f7-navbar back-link="Back">
      <f7-nav-title>track list</f7-nav-title>
      <f7-nav-right>
        <f7-link popup-open=".popup">Filter</f7-link>
      </f7-nav-right>
    </f7-navbar>

    <f7-searchbar
      no-shadow
      search-container=".virtual-list"
      search-item="li"
      search-in=".item-creator"
      :disable-button="!$theme.aurora"
    ></f7-searchbar>

    <f7-list
      class="searchbar-found"
      media-list
      virtual-list
      :virtual-list-params="{ items, searchAll, renderExternal, height: $theme.ios ? 63 : ($theme.md ? 73 : 46)}"
    >
      <ul>
        <f7-list-item
          sheet-open=".sheet"
          v-for="(item, index) in vlData.items"
          :key="index"
          media-item
          @click="getTrackInfo(item.trackName, item.creator, item.level, item.fwBw)"
          link="#"
          :title="item.trackName"
          :text="item.creator"
          :after="'N'+item.level"
          :style="`top: ${vlData.topPosition}px`"
        ></f7-list-item>
      </ul>
    </f7-list>
    <f7-sheet class="sheet" style="height:auto; --f7-sheet-bg-color: #fff;" swipe-to-close backdrop>
      <f7-page-content>
        <f7-block-title class="text-color-primary" large>{{ selectedTrackName }}</f7-block-title>
        <f7-block>
          <h3>
            Track Creator:
            <span class="text-color-primary">{{ selectedCreator }}</span>
          </h3>
          <h3>
            Ninja Level:
            <span class="text-color-primary">{{ level }}</span>
          </h3>

          <h4>
            More Tracks:
            <span class="text-color-primary">{{ tracksAmount }}</span>
          </h4>

          <h5>
            BW:
            <span :style="{ color: colorChange }">{{ bw }}</span>
          </h5>
          <f7-row class="whiteSpace"></f7-row>

          <f7-button
            sheet-close
            @click="moreBy(selectedCreator)"
            outline
            round
          >more by {{ selectedCreator }}</f7-button>

          <f7-row class="whiteSpace"></f7-row>
        </f7-block>
      </f7-page-content>
    </f7-sheet>
    <f7-popup class="popup" :opened="popupOpened" @popup:closed="popupOpened = false">
      <f7-page>
        <f7-navbar title="Search Tracks">
          <f7-nav-right>
            <f7-link popup-close>Close</f7-link>
          </f7-nav-right>
        </f7-navbar>

        <f7-block>
          <h4>Filter Tracks</h4>

          <f7-list no-hairlines-md>
            <f7-list-input
              defaultValue="all"
              @input="ninjaLevel = $event.target.value"
              label="Ninja Level"
              type="select"
            >
              <option value="all">All</option>
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
          <f7-list defaultValue="both" no-hairlines-md clear-button>
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
          <f7-row>
            <f7-col>
              <f7-button popup-close @click="filterTracks" round outline>Filter tracks</f7-button>
            </f7-col>
          </f7-row>
        </f7-block>
      </f7-page>
    </f7-popup>
  </f7-page>
</template>

<script>
import trackList from "@/js/trialsTracks.js";
export default {
  components: {},
  created() {},

  data() {
    const items = [];
    trackList.forEach(x => {
      items.push({
        creator: x.creator,
        trackName: x.trackName,
        level: x.level,
        fwBw: x.fwBw
      });
    });

    return {
      popupOpened: false,
      trackName: "",
      creator: "",
      ninjaLevel: "all",
      fwBw: "both",
      selectedTrackName: "",
      selectedCreator: "",
      level: "",
      bw: "",

      nameSearchArray: [],
      trackSearchArray: [],
      items,

      vlData: {
        items: []
      },
      tracks: "All"
    };
  },
  methods: {
    searchAll(query, items) {
      const found = [];

      for (let i = 0; i < items.length; i += 1) {
        if (
          items[i].creator.toLowerCase().indexOf(query.toLowerCase()) >= 0 ||
          query.trim() === ""
        )
          found.push(i);
        if (
          items[i].trackName.toLowerCase().indexOf(query.toLowerCase()) >= 0 ||
          query.trim() === ""
        )
          found.push(i);
      }
      return found; 
    },
    renderExternal(vl, vlData) {
      this.vlData = vlData;
    },
    getTrackInfo(track, creator, level, bw) {
      this.selectedTrackName = track;
      this.selectedCreator = creator;
      this.level = level;
      this.bw = bw;
    },
    filterTracks() {
      let theList = this.$f7.virtualList.get();
      let tracks = [],
        temp = [];

      if (this.ninjaLevel == "all") {
        trackList.forEach(x => temp.push(x));
      } else {
        trackList.forEach(x => {
          if (x.level === this.ninjaLevel) temp.push(x);
        });
      }

      if (this.fwBw == "both") {
        temp.forEach(x => tracks.push(x));
      } else {
        temp.forEach(x => {
          if (x.fwBw === this.fwBw) tracks.push(x);
        });
      }
      this.vlData.items = tracks;
      theList.replaceAllItems(tracks);
    },
    reset() {
      let theList = this.$f7.virtualList.get();

      theList.replaceAllItems(trackList);
    },
    moreBy(name) {
      let theList = this.$f7.virtualList.get();

      let items = trackList.filter(x => x.creator == name);

      theList.replaceAllItems(items);
      this.vlData.items = items;
    }
  },
  computed: {
    colorChange() {
      if (this.bw == "Yes") {
        return "green";
      } else {
        return "red";
      }
    },
    tracksAmount() {
      let tracks = trackList.filter(x => x.creator == this.selectedCreator)
        .length;

      return tracks;
    }
  }
};
</script>

<style scoped>
.whiteSpace {
  height: 10px;
}
</style>

