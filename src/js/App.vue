<template>
  <section class="app__container">
    <div class="app__header">
      <p class="title">
        Active: <span v-for="ap in activePointer">{{ pointers[ap].name }}</span>
      </p>
      <button type="button" name="button" @click="addPointer({name: 'Unnamed', active: false, positionX: randomCoordinate(), positionY: randomCoordinate()})">Add Pointer</button>
      <p>1117 -268 568</p>
      <input type="text" name="searchInput" v-model="searchInput" placeholder="X Z Y">
      parsed: {{ searchPointer }}
    </div>

    <div class="columns">
      <div class="column is-9">
        <worldmap :pointers="pointers" @addPointerEmit="addPointer" @setActivePointerEmit="addActivePointer"></worldmap>
      </div>
      <div class="column is-3">
        <sidemenu :pointers="pointers" @setActivePointerEmit="addActivePointer"></sidemenu>
      </div>
    </div>
    <!-- <code>
      {{ $options.locations }}
    </code> -->
    <code>
      <span v-for="p in pointers">{{ p }}</span>
    </code>
  </section>
</template>

<script>
  import Worldmap from './components/Worldmap.vue'
  import Sidemenu from './components/Sidemenu.vue'
  import locationsData from '../assets/locations.json';

  export default {
    locations: locationsData,
      data() {
          return {
            pointers: [
              {
                name: 'Wrack 1',
                active: false,
                positionX: 500,
                positionY: 1500,
                positionZ: -410,
                category: 'Cave'
              },
            ],
            activePointer: [],
            searchInput: ''
          }
      },
      computed: {
        searchPointer: function() {
          let temp = this.searchInput.split(' ');
          return {
            name: 'Search Pointer',
            active: true,
            positionX: temp[0],
            positionY: temp[2],
            positionZ: temp[1],
            category: 'search'
          }
        },
        // allPointers: function() {
        //   let returnPointers = JSON.parse(JSON.stringify(this.pointers));
        //   if (this.searchInput) {
        //     returnPointers.push(this.searchPointer);
        //   }
        //   return returnPointers;
        // }
      },
      components: { Worldmap, Sidemenu },
      methods: {
        addPointer: function(pointer) {
          this.pointers.push(pointer);
        },
        addActivePointer: function(index) {
          let actIndex = this.activePointer.indexOf(index);
          if (actIndex >= 0) {
            this.pointers[index].active = false;
            this.activePointer.splice(actIndex, 1);
          }
          else {
            this.pointers[index].active = true;
            this.activePointer.push(index)
          }
        },
        randomCoordinate() {
          return Math.floor((Math.random() * 3000) - 1500);
        },
        importJSON() {
          let tempLoc = [];
          for (let i = 0; i < locationsData.length; i++) {
            let tempCoordinates = locationsData[i].coordinates.split(' ');
            tempLoc.push({
              name: locationsData[i].name,
              active: false,
              positionX: tempCoordinates[0],
              positionY: tempCoordinates[2],
              positionZ: tempCoordinates[1],
              category: locationsData[i].category
            })
          }
          this.pointers = tempLoc;
        }
      },
      created() {
        // this.pointers = this.pointers.concat(locationsData);
        // this.pointers = locationsData;
        this.importJSON();
      }
  }
</script>

<style>
  .app__header {
    margin-bottom: 2em;
  }
</style>
