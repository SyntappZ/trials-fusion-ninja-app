<template>
  <f7-app :params="f7params">
    <!-- Status bar overlay for fullscreen mode-->
    <f7-statusbar></f7-statusbar>

    <!-- Left panel with cover effect-->
   <navbar />

    <!-- Your main view, should have "view-main" class -->
    <f7-view main class="safe-areas" url="/"></f7-view>
  </f7-app>
</template>
<script>
import cordovaApp from "../js/cordova-app.js";
import routes from "../js/routes.js";
import navbar from '../components/Navbar'

export default {
  components: {
    navbar
  },
  data() {
    return {
      // Framework7 Parameters
      f7params: {
        id: "io.syntappz.fusion", // App bundle ID
        name: "fusion-ninja", // App name
        theme: "auto", // Automatic theme detection
        // App root data
        data: function() {
          return {
          
          };
        },

        // App routes
        routes: routes,

        // Input settings
        input: {
          scrollIntoViewOnFocus: this.$device.cordova && !this.$device.electron,
          scrollIntoViewCentered: this.$device.cordova && !this.$device.electron
        },
        // Cordova Statusbar settings
        statusbar: {
          overlay: (this.$device.cordova && this.$device.ios) || "auto",
          iosOverlaysWebView: true,
          androidOverlaysWebView: false
        }
      },

     
    };
  },
  methods: {
   
  },
  mounted() {
    this.$f7ready(f7 => {
      // Init cordova APIs (see cordova-app.js)
      if (f7.device.cordova) {
        cordovaApp.init(f7);
      }
      // Call F7 APIs here
    });
  }
};
</script>