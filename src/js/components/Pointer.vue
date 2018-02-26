<template>
  <div :style="position" :class="['worldmap__pointer', pointerColor, pointerStyle]">
    <div :class="['tooltip', {'is-tooltip-active': pointerData.active}]" :data-tooltip="pointerData.name + ' (' + pointerData.positionX + ', ' + pointerData.positionZ + ', ' + pointerData.positionY + ')'">
      <div class="image is-24x24">
        <svg fill="#000000" height="24" viewBox="0 0 24 24" width="24" xmlns="http://www.w3.org/2000/svg">
            <path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7zm0 9.5c-1.38 0-2.5-1.12-2.5-2.5s1.12-2.5 2.5-2.5 2.5 1.12 2.5 2.5-1.12 2.5-2.5 2.5z"/>
            <path d="M0 0h24v24H0z" fill="none"/>
        </svg>
      </div>
    </div>
  </div>
</template>

<script>
    export default {
        data() {
            return { }
        },
        computed: {
          position: function() {
            return {
              left: this.translateCoordinate(this.pointerData.positionX) + '%',
              bottom: this.translateCoordinate(this.pointerData.positionY) + '%',
            }
          },
          pointerStyle: function() {
            return {
              'worldmap__pointer--active': this.pointerData.active,
            }
          },
          pointerColor: function() {
            return 'worldmap__pointer--' + this.pointerData.category.toLowerCase();
          }
        },
        props: ['pointerData'],
        methods: {
          translateCoordinate: function(val) {
            return (val / 40) + 50;
          }
        }
    }
</script>

<style>
  .worldmap__pointer {
    position: absolute;
    height: 24px;
    width: 24px;
    margin-left: -12px;
    /* z-index: 1; */
    cursor: pointer;
  }
  .worldmap__pointer svg {
    filter: drop-shadow( 0px 0px 3px #e6e6e6 );
  }
  .worldmap__pointer--wreck svg {
    fill: #3f51b5;
  }
  .worldmap__pointer--wreck:hover svg {
    fill: #243492;
  }
  .worldmap__pointer--cave svg {
    fill: #795548;
  }
  .worldmap__pointer--cave:hover svg {
    fill: #4e3a33;
  }
  .worldmap__pointer--search svg {
    fill: #9c27b0;
  }
  .worldmap__pointer--search:hover svg {
    fill: #7a128c;
  }
  .worldmap__pointer--spawn svg {
    fill: #ff9800;
  }
  .worldmap__pointer--spawn:hover svg {
    fill: #bb7206;
  }
  .worldmap__pointer--seabase svg {
    fill: #4caf50;
  }
  .worldmap__pointer--seabase:hover svg {
    fill: #2d7730;
  }
  .worldmap__pointer--active svg {
    fill: #e91e63!important;
  }
</style>
