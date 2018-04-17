<template>
  <div class="pane"
       @click="addChild"
       :style="{ minWidth: '10%', maxWidth: '90%'}">
  </div>
</template>
<script>
/* eslint-disable no-underscore-dangle */

import { Multipane, MultipaneResizer } from 'vue-multipane';

export default{
  name: 'pane',
  components: {
    Multipane,
    MultipaneResizer,
  },
  methods: {
    addChild() {
      let id;
      if (this._uid === 3) {
        id = 0;
      } else {
        id = this._uid - 4;
      }
      // eslint-disable-next-line
      console.log("Child ID -> ", id);
      this.$emit('addChild', id);
    },
  },
};
</script>

<style>
  .pane {
    text-align: left;
    /*padding: 15px;*/
    overflow: hidden;
    background: #eee;
    border: 1px solid #000000;
    height: 100%;
  }
  .layout-v > .multipane-resizer {
    height: 40px;
  }
  .layout-h > .multipane-resizer {
    height: 40px;
  }
  .multipane-resizer {
    margin: 0;
    display: block;
    width: 5px;
    height: 40px;
    left: 0px;
    margin-top: 175px;
    margin-left: 5px;
    margin-right: 5px;
    border-left: 1px solid #ccc;
    border-right: 1px solid #ccc;
  }
</style>
