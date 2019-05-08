<template>
  <f7-panel left sliding cover>
    <f7-view>
      <f7-page>
        <f7-navbar title="Menu"></f7-navbar>
        
          <f7-list>
        <f7-list-item
          link="/"
          title="Home"
          link-view="#main-view"
          panel-close
          reload-all
        />
        <f7-list-item
          link="/trackList/"
          title="Track List"
          link-view="#main-view"
          panel-close
          reload-all
        />
      </f7-list>
        
         <button  class="col button color-black auth">Syntappz</button>
         
        
      </f7-page>
    </f7-view>
  </f7-panel>
</template>

<script>


export default {
  data() {
    return {

    }
  },
  methods: {
    changePage(page) {
    
    }
  }
}
</script>


<style scoped>
.size-20 {
  font-size: 20px;
}
.auth {
  position: absolute;
  bottom: 0;
  height:10vh;
}

</style>
