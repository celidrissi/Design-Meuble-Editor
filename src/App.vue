<template>
  <div id="App">
    <h2>Insertion dynamique</h2>
    <multipane
      class="custom-resizer"
      layout="Horizontal"
      :label="tree.label"
      :asresizer="tree.asresizer"
      :asnodes="tree.asnodes"
      :nodes="tree.nodes"
    >
      <div ref="container">
        <button @click="addChild">Ajouter Ligne</button>
      </div>
      <div ref="container1">
        <button @click="addBrother">Ajouter Ligne</button>
      </div>
      <!--<pane-->
        <!--@click.native="onClick"-->
      <!--&gt;-->
        <!--Cliquer 0-->
      <!--</pane>-->
      <!--<multipane-resizer-->
        <!--class="multipane-resizer"/>-->
      <!--<pane-->
        <!--v-on:click="onClick()"-->
        <!--:style="{flexGrow: 1 }">-->
        <!--<div></div>-->
        <!--Cliquer 1-->
      <!--</pane>-->
    </multipane>
  </div>
</template>

<script>
import { Multipane, MultipaneResizer } from 'vue-multipane';
import Vue from 'vue';
import Pane from './components/Pane';
import swal from '../node_modules/sweetalert';
import Button from './components/Button';


export default {
  name: 'App',
  components: {
    Multipane,
    MultipaneResizer,
    Pane,
    Button,
  },
  data() {
    return {
      tree: {
        label: '0',
        asresizer: false,
        asnodes: true,
        nodes: [],
      },
    };
  },
  methods: {
    addChild() {
      swal('Ligne Ajouté');
      const ComponentClass = Vue.extend(Pane);
      const instance = new ComponentClass({
        propsData: { type: 'primary' },
      });
      instance.$slots.default = ['Clique moi !'];

      // eslint-disable-next-line
      console.log(this.$refs);
      instance.$mount(); // pass nothing
      this.$refs.container.appendChild(instance.$el);
    },
    addBrother() {
      swal('Ligne Ajouté');
      const ComponentClass = Vue.extend(Pane);
      const instance = new ComponentClass({
        propsData: { type: 'primary' },
      });
      instance.$slots.default = ['Clique moi !'];

      // eslint-disable-next-line
      console.log(this.$refs);
      instance.$mount(); // pass nothing
      this.$refs.container.addChild(instance.$el);
    },
  },
};
</script>
<style scoped>
  .custom-resizer {
    width: 100%;
    height: 400px;
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
