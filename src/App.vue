<template>
  <div id="App">
    <MultiPaneBox :panes="panes" :type="vertical"/>
  </div>
</template>

<script>
// import swal from 'sweetalert';
import { Multipane, MultipaneResizer } from 'vue-multipane';
// import Vue from 'vue';
import MultiPaneBox from './components/MultipaneBox';


export default {
  name: 'App',
  components: {
    Multipane,
    MultipaneResizer,
    MultiPaneBox,
  },
  data() {
    return {
      panes: [
        {
          childs: [
          ],
        },
        {
          childs: [
          ],
        },
      ],
    };
  },
};
</script>
<style>
  html, body, #App {
    height: 100%;
  }
</style>
