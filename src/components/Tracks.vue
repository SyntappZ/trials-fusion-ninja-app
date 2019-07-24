<template>
  <f7-page>
  
    
  <f7-block-title>Tracks</f7-block-title>
    <f7-list
      class="searchbar-found"
      media-list
      virtual-list
      :virtual-list-params="{ items, searchAll, renderExternal, height: $theme.ios ? 63 : ($theme.md ? 73 : 46)}"
    >
      <ul>
        <f7-list-item class="title-text-color-primary"
          v-for="(item, index) in vlData.items"
          :key="index"
          media-item
          link="#"
          :title="item.title"
          :subtitle="item.subtitle"
           :after="'N' + item.level"
           :text="'fwbw - ' + item.bw"
          :style="`top: ${vlData.topPosition}px`"
        ></f7-list-item>
      </ul>
    </f7-list>
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
          title: x.creator,
          subtitle: x.trackName,
          level: x.level,
          bw: x.fwBw
        })
      })
      
      
      return {
        items,
        vlData: {
          items: [],
        },
      };
    },
    methods: {
     
      searchAll(query, items) {
        const found = [];
        for (let i = 0; i < items.length; i += 1) {
          if (items[i].title.toLowerCase().indexOf(query.toLowerCase()) >= 0 || query.trim() === '') found.push(i);
        }
        return found; // return array with mathced indexes
      },
      renderExternal(vl, vlData) {
        this.vlData = vlData;
      },
    },
 
};
</script>
<style scoped>

</style>


