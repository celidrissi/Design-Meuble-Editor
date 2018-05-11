<template>
  <div class="pane"
       :style="{ minWidth: '10%', maxWidth: '90%', flexGrow: '1' }"
       ref="setref()">
    <button @click="addChild" class="button">| |</button>
  </div>
</template>
<script>
import swal from 'sweetalert';
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
    randomColor() {
      const colors = ['#C44C51', '#8CC6D7', '#FFDA8C', '#006D80', '#BDA44D', '#3C2000'];
      return colors[Math.floor(Math.random() * colors.length)];
    },
    addChild() {
      const id = this.$el.children.length - 1;
      // On verifie si on atteint le seuil
      if (id >= 6) {
        swal('Too many child');
        return;
      }

      // eslint-disable-next-line
      console.log('-----------------------------------------------------');
      const ComponentClass = Vue.extend(Pane);
      const ComponentClassRes = Vue.extend(MultipaneResizer);
      const instance = new ComponentClass({
        propsData: { type: 'primary' },
      });
      const instanceRes = new ComponentClassRes({
        propsData: { type: 'primary' },
      });

      // On recupere les éléments ayant pour class pane et on verifie si on atteint le seuil
      // const panes = document.getElementsByClassName('pane');
      instance.$mount(); // pass nothing
      instanceRes.$mount();

      // eslint-disable-next-line
      console.log("this -> ", this);
      // eslint-disable-next-line
      console.log("this.$el.children -> ",this.$el.children);
      // eslint-disable-next-line
      // console.log("panes -> ", panes);
      // eslint-disable-next-line
      // console.log("Children Length -> ",this.children.length);
      if (id >= 1) {
        // eslint-disable-next-line
        console.log("Res !!");
        this.$el.appendChild(instanceRes.$el);
      }
      this.$el.appendChild(instance.$el);

      // eslint-disable-next-line
      console.log(" // ", id);
      if (id >= 2) {
        if (this.$el.children[id].style.flexGrow === '1') {
          // eslint-disable-next-line
          console.log("// ", this.$el.children[id].style.flexGrow);
        }
      }
    },
  },
};
</script>
<style>
  .pane {
    text-align: left;
    padding-left: 10px;
    padding-top: 10px;
    padding-right: 10px;
    overflow: hidden;
    background: #eee;
    border: 1px solid #000000;
    height: 100%;
    display: flex;
  }
  .pane > button {
    position: absolute;
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
