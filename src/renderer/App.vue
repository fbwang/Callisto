<template>
  <div id="app">
    <!--<landing-page></landing-page>-->
    <template-file></template-file>
    <!--<data-file></data-file>-->
  </div>
</template>

<script>
  // import LandingPage from "./components/LandingPage";

  import TemplateFile from "./components/TemplateFile";
  // import DataFile from "./components/TemplateFile/DataFile";
  export default {
    name: 'callisto',
    components: {
        // DataFile,
        TemplateFile
        // LandingPage,
    }
  }
</script>

<style>
  /* CSS */
</style>
