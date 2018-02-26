<template>
  <div class="panel">
    <div class="panel-heading">
      settings
    </div>
    <div class="panel-block">
      <p class="control has-icons-left">
        <input class="input is-small" type="text" name="" v-model="searchInput" placeholder="search">
        <span class="icon is-small is-left">
            <svg fill="#c7c7c7" height="24" viewBox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg">
                <path d="M15.5 14h-.79l-.28-.27C15.41 12.59 16 11.11 16 9.5 16 5.91 13.09 3 9.5 3S3 5.91 3 9.5 5.91 16 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/>
                <path d="M0 0h24v24H0z" fill="none"/>
            </svg>
        </span>
      </p>
    </div>
    <!-- <a @click="coordinates.xCoordinate = 364; coordinates.yCoordinate = 310;" class="panel-block">Lifepod 14</a> -->
    <a :class="['panel-block', {'is-active':pointer.active}]" v-for="(pointer, index) in filteredPointers" @click="setActivePointerEmit(index)">
      <span class="panel-icon" v-if="!pointer.active">
        <i class="icon is-small">
          <svg v-bind:fill="colors[pointer.category.toLowerCase()]" height="24" viewBox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg">
            <path d="M0 0h24v24H0z" fill="none"/>
            <path d="M20.94 11c-.46-4.17-3.77-7.48-7.94-7.94V1h-2v2.06C6.83 3.52 3.52 6.83 3.06 11H1v2h2.06c.46 4.17 3.77 7.48 7.94 7.94V23h2v-2.06c4.17-.46 7.48-3.77 7.94-7.94H23v-2h-2.06zM12 19c-3.87 0-7-3.13-7-7s3.13-7 7-7 7 3.13 7 7-3.13 7-7 7z"/>
          </svg>
        </i>
      </span>
      <span class="panel-icon" v-else>
        <i class="icon is-small">
          <svg fill="#e91e63" height="24" viewBox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg">
              <path d="M0 0h24v24H0z" fill="none"/>
              <path d="M12 8c-2.21 0-4 1.79-4 4s1.79 4 4 4 4-1.79 4-4-1.79-4-4-4zm8.94 3c-.46-4.17-3.77-7.48-7.94-7.94V1h-2v2.06C6.83 3.52 3.52 6.83 3.06 11H1v2h2.06c.46 4.17 3.77 7.48 7.94 7.94V23h2v-2.06c4.17-.46 7.48-3.77 7.94-7.94H23v-2h-2.06zM12 19c-3.87 0-7-3.13-7-7s3.13-7 7-7 7 3.13 7 7-3.13 7-7 7z"/>
          </svg>
        </i>
      </span>
      {{ pointer.name }} ({{ pointer.positionX }}, {{ pointer.positionY }})
    </a>
    <!-- <div class="panel-block">
      <switcher label="Wrecks" checked="true" id="wrecks"></switcher>
    </div>-->
    <div class="panel-block">
      <button class="button is-link is-outlined is-fullwidth" @click="coordinates.xCoordinate = 0; coordinates.yCoordinate = 0;">
        reset all filters
      </button>
    </div>
  </div>
</template>

<script>
    export default {
      data() {
          return {
            colors: {
              'wreck': '#3f51b5',
              'cave': '#795548',
              'search': '#9c27b0',
              'spawn': '#ff9800',
              'seabase': '#4caf50'
            },
            searchInput: ""
          }
      },
      props: ['pointers'],
      methods: {
        setActivePointerEmit: function(index) {
          this.$emit('setActivePointerEmit', index);
        }
      },
      computed: {
        filteredPointers: function() {
          return this.pointers.filter(point => {
            return point.name.toLowerCase().includes(this.searchInput.toLowerCase()) || point.category.toLowerCase().includes(this.searchInput.toLowerCase())
          })
        }
      }
    }
</script>

<style>
  .panel-block.is-active {
    background-color: whitesmoke;
  }
</style>
