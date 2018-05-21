<template>
    <div :style="{height: '100%', width: '100%'}">
      <button v-if="showButton" v-on:click="createPane()">||</button>
      <button v-if="showButton" v-on:click="deletePane()">x</button>
      <multipane
        class="custom-multipane"
        layout="vertical"
      >
        <template v-for="(pane, index) in panes">
          <Pane
            :pane="pane"
            :is-last="index === panes.length - 1"
            :min-width="10"
            :max-width="90"
            :key="index"
            v-on:display-button="displayButton(false)"
          />
          <multipane-resizer
            v-if="index + 1 < panes.length"
            v-on:mouseup="newWidth = 100 - width"
            :key="'resize' + index"/>
        </template>
      </multipane>

    </div>
</template>

<script>
/* eslint-disable no-console */
// import swal from 'sweetalert';
import { Multipane, MultipaneResizer } from 'vue-multipane';


export default {
  name: 'MultiPaneBox',
  data() {
    return {
      showButton: true,
      newWidth: 0,
    };
  },
  props: {
    panes: {
      type: Array,
      required: true,
    },
  },
  components: {
    Multipane,
    MultipaneResizer,
    Pane: () => import('./Pane.vue'),
  },
  methods: {
    createPane() {
      this.panes.push({
        childs: [],
      });
    },
    deletePane(id) {
      this.$emit('delete-child', id);
    },
    displayButton(state) {
      if (state !== undefined) {
        if (this.panes.length === 2) {
          this.showButton = false;
        }
        this.$emit('display-button', state);
        console.log('emit 2 ! + ');
      }
    },
  },
};

</script>

<style>
  .custom-multipane {
    width: 100%;
    height: 100%;
  }
  .layout-v .multipane-resizer {
    cursor: col-resize;
    margin: auto;
    height: 100px;
    width: 4px;
    display: block;
    left: 2px;
    margin-left: 0px;
    margin-top: 300px;
    border-left: 10px solid #ffb100;
  }
  .button1 {
    margin-left: 20px;
  }
</style>
