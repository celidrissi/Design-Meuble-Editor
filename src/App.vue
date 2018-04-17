<template>
  <div id="App">
    <h2>Insertion dynamique</h2>
    <button v-on:click="nbPane++, setResizer=!setResizer">
      Ajouter Colonne
    </button>  NB Colonnes : {{ this.nbPane }}
    <multipane
      class="custom-resizer"
      v-on:click="addChild()"
      layout="vertical"
      ref="container"
    >
      <div v-for="n in nbPane">
        <pane v-on:addChild="addChild"/>
        <multipane-resizer v-if="setResizer"/>
      </div>
    </multipane>
  </div>
</template>

<script>
import swal from 'sweetalert';
import { Multipane, MultipaneResizer } from 'vue-multipane';
// import Vue from 'vue';
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
  data() {
    return {
      nbPane: 0,
      setResizer: true,
    };
  },
  methods: {
    addChild() {
      // eslint-disable-next-line
      console.log("-> ", this.nbPane % 2);
      if (this.nbPane % 2 === 0) {
        swal('1');
        this.setResizer = true;
      }
      this.nbPane += 1;

      swal('This Is Your Child !');
      // const identity = document.getElementsByClassName('custom-resizer');
      //
      // const ComponentClass = Vue.extend(Pane);
      // const ComponentClassRes = Vue.extend(MultipaneResizer);
      // const instance = new ComponentClass({
      //   propsData: { type: 'primary' },
      // });
      // const instanceRes = new ComponentClassRes({
      //   propsData: { type: 'primary' },
      // });
      //
      // // eslint-disable-next-line
      // // console.log(this.$refs);
      // instance.$mount(); // pass nothing
      // instanceRes.$mount();
      //
      //
      // // eslint-disable-next-line
      // console.log("Instance ",instance);
      // // // eslint-disable-next-line
      // // console.log("ID -> ",identity[0].childElementCount);
      // if (identity[0].childElementCount !== 0) {
      //   identity[0].appendChild(instanceRes.$el);
      // }
      // identity[0].setAttribute('v-on:addChild', 'this.addChild');
      // identity[0].appendChild(instance.$el);
      //
      // // eslint-disable-next-line
      // console.log("Test -> ", identity[0]);
      // // eslint-disable-next-line
    },
  },
};
</script>
<style scoped>
  #app {
    width: 100%;
    height: 100%;
  }

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
