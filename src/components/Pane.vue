<template>
  <div class="pane"
       @click="addChild"
       :style="{ minWidth: '10%', maxWidth: '90%', flexGrow: '1' }">
  </div>
</template>
<script>
/* eslint-disable no-underscore-dangle */
import { Multipane, MultipaneResizer } from 'vue-multipane';
import Vue from 'vue';
import Pane from './Pane';
// import Button from './Button';

export default{
  name: 'pane',
  components: {
    Multipane,
    MultipaneResizer,
    Pane,
  },
  methods: {
    addChild() {
      // eslint-disable-next-line
      console.log('----------------------------------------------------');
      const ComponentClass = Vue.extend(Pane);
      const ComponentClassRes = Vue.extend(MultipaneResizer);
      const instance = new ComponentClass({
        propsData: { type: 'primary' },
      });
      const instanceRes = new ComponentClassRes({
        propsData: { type: 'primary' },
      });

      // On recupere les éléments ayant pour class pane et on verifie si on atteint le seuil
      const panes = document.getElementsByClassName('pane');

      instance.$mount(); // pass nothing
      instanceRes.$mount();
      // eslint-disable-next-line
      console.log("This -> ", this);
      // eslint-disable-next-line
      console.log("Children -> ",this.children);
      // eslint-disable-next-line
      console.log("Panes -> ", panes);
      // eslint-disable-next-line
      console.log("This Panes -> ", panes[this._uid-3]);
      // eslint-disable-next-line
      // console.log("Children Length -> ",this.children.length);
      if (this.children !== undefined) {
        this.addChild(instanceRes.$el);
      }
      this.addChild(instance.$el);

      if (this.children.length >= 3) {
        // eslint-disable-next-line
        console.log("// ",
          this.children[this.children.length - 3]);
        // eslint-disable-next-line
        if (this.children[this.children.length - 3].style.flexGrow == "1") {
          this.children[this.children.length - 3].style.flexGrow = '0';
        }
      }
    },
  },
};
</script>
cos
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
    margin-top: 250px;
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
