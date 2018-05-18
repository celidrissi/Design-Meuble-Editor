<template>
  <div id="App">
    <MultiPaneBox is :panes="panes"/>
  </div>
</template>

<script>
// import swal from 'sweetalert';
import { Multipane, MultipaneResizer } from 'vue-multipane';
// import Vue from 'vue';
import MultiPaneBox from './components/MultiPaneBox';

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
            {
              childs: [],
            },
            {
              childs: [],
            },
          ],
        },
      ],
    };
  },
};
</script>
<style>
</style>
