<template>
  <f7-page name="home">
    <background />

    <!-- Top Navbar -->
    <f7-navbar :sliding="false">
      <f7-nav-left>
        <f7-link icon-ios="f7:menu" icon-aurora="f7:menu" icon-md="material:menu" panel-open="left"></f7-link>
      </f7-nav-left>
      <f7-nav-title sliding>Trials Fusion Ninja</f7-nav-title>
    </f7-navbar>
  
   

  </f7-page>
</template>

<script>
import background from '../components/Background'
export default {
  components: {
    background
  }
}
</script>
