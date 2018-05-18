<template>
  <div
    class="pane"
    :style="{
    width: width.toString()+'%',
    minWidth: minWidth.toString()+'%' ,
    maxWidth: maxWidth.toString()+'%' ,
    flexGrow: isLast ? '1' : '0'}">
      <MultiPaneBox :panes="panex.childs"/>
  </div>
</template>
<script>
import MultiPaneBox from './MultiPaneBox';
// import swal from 'sweetalert';

export default{
  name: 'pane',
  props: {
    panex: {
      type: Object,
      required: true,
    },
    isLast: {
      type: Boolean,
      required: true,
    },
    width: {
      type: Number,
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
</style>
