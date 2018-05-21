<template>
  <div
    class="pane"
    :style="{
    minWidth: minWidth.toString()+'%' ,
    maxWidth: maxWidth.toString()+'%' ,
    flexGrow: isLast ? '1' : '0'}">
      <MultiPaneBox :panes="pane.childs" :type="type" v-on="displayButton(false)"/>
  </div>
</template>
<script>
/* eslint-disable no-console */
// import swal from 'sweetalert';
import MultiPaneBox from './MultipaneBox';


export default{
  name: 'pane',
  props: {
    pane: {
      type: Object,
      required: true,
    },
    type: {
      type: String,
      required: true,
    },
    isLast: {
      type: Boolean,
      required: true,
    },
    minWidth: {
      type: Number,
      required: true,
    },
    maxWidth: {
      type: Number,
      required: true,
    },
  },
  components: {
    MultiPaneBox,
  },
  methods: {
    displayButton(state) {
      if (state !== undefined) {
        this.$emit('display-button', state);
        console.log('emit 1 !');
      }
    },
  },
};
</script>

<style>
  .pane {
    overflow: hidden;
    background: #eee;
    border: 1px solid #000000;
    height: 100%;
  }
</style>
