<template>
    <div class="worldmap">
      <!-- <button type="button" name="button" @click="addPointerEmit(Math.floor((Math.random() * 3000) - 1500), Math.floor((Math.random() * 3000) - 1500))">Add Pointer</button> -->

      <div class="worldmap__container">
        <div class="image is-1by1 worldmap__map">
          <img src="images/map.png" alt="">
        </div>
        <pointer v-for="(item, index) in pointers" :key="index" :pointer-data="item" @click.native="setActivePointerEmit(index)"></pointer>
      </div>
      <!-- <ul>
        <li v-for="(pointer, index) in pointers">{{ index + 1 }}: x = {{ pointer.positionX }} y = {{ pointer.positionY }}</li>
      </ul> -->
    </div>
</template>

<script>
    import Pointer from './Pointer.vue'


    export default {
        data() {
            return {
            }
        },
        props: ['pointers'],
        components: { Pointer },
        methods: {
          translateCoordinate: function(val) {
            return (val / 40) + 50;
          },
          addPointerEmit: function(positionX, positionY) {
            this.$emit('addPointerEmit', {positionX: positionX, positionY: positionY});
          },
          setActivePointerEmit: function(index) {
            this.$emit('setActivePointerEmit', index);
          }
        }
    }
</script>

<style>
    .worldmap__container {
      position: relative;
    }
    .worldmap__map > img {
      filter: brightness(180%);
      opacity: 0.5;
    }
</style>
