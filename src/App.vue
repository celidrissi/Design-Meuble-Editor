<template>
  <div id="App">
    <h2>Insertion dynamique</h2>
    <button @click="addChild()">Ajouter Colonne</button>
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
import Button from './components/Button';


export default {
  name: 'App',
  components: {
    Multipane,
    MultipaneResizer,
    Pane,
    Button,
  },
  methods: {
    addChild(id) {
      swal('I Making Child');
      let identity;
      if (id !== undefined) {
        identity = 0;
      } else {
        identity = document.getElementsByClassName('custom-resizer');
      }

      const ComponentClass = Vue.extend(Pane);
      const ComponentClassRes = Vue.extend(MultipaneResizer);
      const instance = new ComponentClass({
        propsData: { type: 'primary' },
      });
      const instanceRes = new ComponentClassRes({
        propsData: { type: 'primary' },
      });

      // eslint-disable-next-line
      // console.log(this.$refs);
      instance.$mount(); // pass nothing
      instanceRes.$mount();

      // eslint-disable-next-line
      console.log("This -> ", this);
      // eslint-disable-next-line
      console.log("Instance ",identity[0]);
      // eslint-disable-next-line
      console.log("ID -> ",identity[0].childElementCount);
      if (identity[0].childElementCount !== 0) {
        identity[0].appendChild(instanceRes.$el);
      }
      identity[0].appendChild(instance.$el);
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
