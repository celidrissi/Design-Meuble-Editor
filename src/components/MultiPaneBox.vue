<template>
    <div>
      <button v-on:click="createPane()">
        Ajouter Colonne
      </button>
      <multipane
        class="custom-multipane"
        layout="vertical"
      >
        <template v-for="(pane, index) in panes">
          <Pane
            :panex="pane"
            :is-last="index === panes.length - 1"
            :width="100 / panes.length"
            :min-width="100 / 10"
            :max-width="100 - (10 * panes.length)"
            :key="index"/>
          <multipane-resizer v-if="index + 1 < panes.length" :key="'resize' + index"/>
        </template>
      </multipane>
    </div>
</template>

<script>
import swal from 'sweetalert';
import { Multipane, MultipaneResizer } from 'vue-multipane';
import Pane from './Pane';

export default {
  name: 'MultiPaneBox',
  props: {
    panes: {
      type: Array,
      required: true,
    },
  },
  components: {
    Multipane,
    MultipaneResizer,
    Pane,
  },
  methods: {
    createPane() {
      this.panes.push({
        childs: [],
      });
      swal('ok');
    },
  },
};

</script>

<style>
  .custom-multipane {
    width: 96%;
    height: 96%;
    position: absolute;
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
