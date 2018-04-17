<template>
  <div class="pane"
       @click="addChild()"
       :style="{ minWidth: '10%', maxWidth: '90%', flexGrow:1}">
    <slot/>
  </div>
</template>
<script>
/* eslint-disable no-underscore-dangle */

import { Multipane, MultipaneResizer } from 'vue-multipane';
import swal from 'sweetalert';

export default{
  name: 'pane',
  components: {
    Multipane,
    MultipaneResizer,
  },
  methods: {
    addChild() {
      swal('I Want A Child !');
      let uid;
      if (this._uid === 3) {
        uid = 0;
      } else {
        uid = this._uid - 4;
      }
      const identity = document.getElementById(uid);
      // eslint-disable-next-line
      console.log("Child ID -> ", this);
      this.$emit('addChild', identity);
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
    width: 4px;
    margin: 0;
    display: block;
    left: 2px;
    margin-top: 45%;
    border-left: 2px solid #ffb100;
  }
  .layout-h > .multipane-resizer {
    height: 40px;
    margin: 0;
    display: block;
    width: 5px;
    left: 0px;
    margin-top: 175px;
    margin-left: 5px;
    margin-right: 5px;
    border-left: 1px solid #ccc;
  }
</style>
<!--
<div class="custom-resizer" layout="vertical" class=""pane>
  &lt;!&ndash; Instancier  par programme &ndash;&gt;
  <pane class="pane"
        v-for="(tree, index) in nodes"
        :key="index"
        :nodes="tree.nodes"
        :label="tree.label"
        :asnodes="tree.asnodes"
        :asresizer="tree.asresizer"
        :slot="resizer"
  />
  <div v-if=!this.asnodes> {{ this.label }} </div>
  <div v-if="!this.asresizer">
    <slot/>
  </div>
  <slot name="resizer">
    {{ this.label }}
    <multipane-resizer/>
  </slot>
</div>
-->
