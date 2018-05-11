<template>
  <div id="App">
    <button @click="addChild()">| |</button>
    <multipane
      class="custom-resizer"
      layout="vertical"
      ref="container"
    >
    </multipane>
  </div>
</template>

<script>
import swal from 'sweetalert';
import { Multipane, MultipaneResizer } from 'vue-multipane';
import Vue from 'vue';
import Pane from './components/Pane';

export default {
  name: 'App',
  components: {
    Multipane,
    MultipaneResizer,
    Pane,
  },
  data() {
    return {
      Vue,
    };
  },
  methods: {
    addChild() {
      // On recupere les éléments ayant pour class pane et on verifie si on atteint le seuil
      const panes = document.getElementsByClassName('pane');
      if (panes.length === 6) {
        swal('Too many child');
        return;
      }

      // eslint-disable-next-line
      console.log('----------------------------------------------------');
      // On recupere les éléments ayant pour class custom-resizer
      const identity = document.getElementsByClassName('custom-resizer');

      const ComponentClass = Vue.extend(Pane);
      const ComponentClassRes = Vue.extend(MultipaneResizer);
      const instance = new ComponentClass({
        propsData: { type: 'primary' },
      });
      const instanceRes = new ComponentClassRes({
        propsData: { type: 'primary' },
      });
      instance.$mount(); // pass nothing
      instanceRes.$mount();

      // Quelques prints
      // eslint-disable-next-line
        console.log("This -> ", this);
      // eslint-disable-next-line
        console.log("Identity ",identity);
      // eslint-disable-next-line
        console.log("Identity Children Count -> ",identity[0].childElementCount);
      // eslint-disable-next-line
        console.log("Panes -> ", panes);

      // Si un enfant existe on ajoute un resizer
      if (identity[0].childElementCount !== 0) {
        identity[0].appendChild(instanceRes.$el);
      }

      //
      if (panes.length > 0) {
        // eslint-disable-next-line
        console.log("The div to change ", panes.length - 1);
        if (panes[panes.length - 1].style.flexGrow === '1') {
          panes[panes.length - 1].style.flexGrow = '0';
        }
        panes[panes.length - 1].style.maxWidth = `${parseInt(panes[panes.length - 1].style.maxWidth, 10) - 10}%`;
      }
      identity[0].appendChild(instance.$el);
    },
  },
};
</script>
<style>
  body{
    width: 100%;
    height: 100%;
  }
  .custom-resizer {
    width: 98%;
    height: 98%;
    position: absolute;
  }
</style>
