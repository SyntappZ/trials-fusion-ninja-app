<template>
  <f7-page>
    <f7-block-title>{{ tracks }}</f7-block-title>
    <f7-list
      class="searchbar-found"
      media-list
      virtual-list
      :virtual-list-params="{ items, renderExternal, height: $theme.ios ? 63 : ($theme.md ? 73 : 46)}"
    >
      <ul>
        <f7-list-item
       
          sheet-open=".sheet"
          v-for="(item, index) in vlData.items"
          :key="index"
          media-item
           @click="getTrackInfo(item.track, item.creator, item.level, item.bw)"
          link="#"
          :title="item.track"
          :text="item.creator"
          :after="'N'+item.level"
          :style="`top: ${vlData.topPosition}px`"
        ></f7-list-item>
      </ul>
     
    </f7-list>
     <f7-sheet
       
        
        class="sheet"
        style="height:auto; --f7-sheet-bg-color: #fff;"
        swipe-to-close
        backdrop
      >
        <f7-page-content>
          <f7-block-title class="text-color-primary" large>{{ trackName }}</f7-block-title>
          <f7-block>
            <h3>Track Creator: 
             
               <span  class="text-color-primary"> {{ creator }}</span>
              </h3>
             <h3>Ninja Level: 
               <span  class="text-color-primary">{{ level }}</span>

             </h3>
          
            <h5>BW: 
              <span :style="{ color: colorChange }">{{ bw }}</span>
            </h5>
         
          </f7-block>
          
           
        </f7-page-content>
      </f7-sheet>
  </f7-page>
</template>

<script>
import trackList from "../js/trialsTracks.js";
export default {
  created() {},
  data() {
    const items = [];
    trackList.forEach(x => {
      items.push({
        creator: x.creator,
        track: x.trackName,
        level: x.level,
        bw: x.fwBw
      });
    });

    return {
      items,
      vlData: {
        items: []
      },
      tracks: "All Tracks",
      trackName: '',
      creator: '',
      level: '',
      bw: ''
    };
  },
  methods: {
    // searchAll(query, items) {
    //   console.log(items)
    //   const found = [];
    //   for (let i = 0; i < items.length; i += 1) {
    //     if (
    //       items[i].title.toLowerCase().indexOf(query.toLowerCase()) >= 0 ||
    //       query.trim() === ""
    //     )
    //       found.push(i);
    //   }
    //   return found; // return array with mathced indexes
    // },
    renderExternal(vl, vlData) {
      
      this.vlData = vlData;
    },
    getTrackInfo(track, creator, level, bw) {
      this.trackName = track
      this.creator = creator
      this.level = level
      this.bw = bw
      
    },
    search() {
     
    }
  },
  computed: {
    colorChange() {
      if(this.bw == 'Yes') {
        return 'green'
      }else{
        return 'red'
      }
    }
  },
  
};
</script>
<style scoped>

</style>


