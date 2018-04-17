<template>
  <div class="pane" :style="{ minWidth: '10%', maxWidth: '90%'}">
    <slot type="label"/>
    <div ref="container">
      <button @click="onClick">Ajouter Ligne</button>
    </div>
  </div>
</template>
<script>
import { Multipane, MultipaneResizer } from 'vue-multipane';
import swal from '../../node_modules/sweetalert';

export default{
  props: ['label', 'nodes', 'asresizer', 'asnodes'],
  name: 'pane',
  components: {
    Multipane,
    MultipaneResizer,
  },
  methods: {
    onClick() {
      swal('Alerte');
      this.$emit('onClick');
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
