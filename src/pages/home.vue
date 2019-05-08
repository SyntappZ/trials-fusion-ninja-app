<template>
  <f7-page name="home">
    <background/>

    <!-- Top Navbar -->
    <f7-navbar>
      <f7-nav-left class="padding">
       
      </f7-nav-left>
      <f7-nav-title>Trials Fusion Ninja</f7-nav-title>
    </f7-navbar>

    <a href="/trackList/">
      <button class="col track-btn button button-fill color-teal">Track list</button>
    </a>

    <div class="block-title">Welcome To Trials The Fusion Ninja App</div>
    <div class="block">
      <div class="block-header">About This App</div>
      <p>This is a fan made app with all the best ninja's of trials fusion. Search tracks/creators or search by ninja level.</p>

      <button class="col button color-black">
        <f7-link href="/about/">More info</f7-link>
      </button>
    </div>
  </f7-page>
</template>

<script>
import background from "../components/Background";

export default {
  components: {
    background
  },
  data() {
    return {};
  },
  methods: {}
};
</script>


<style scoped>
.block-title {
  margin-top: 30vh;
}
.track-btn {
  position: absolute;
  bottom: 0;
  height: 10vh;
}
/* .padding {
  padding-left:40px;
} */
</style>
