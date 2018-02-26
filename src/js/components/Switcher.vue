<template>
  <div class="field">
    <input :id="id" type="checkbox" :name="id" class="switch" v-model="checked">
    <label :for="id">{{ label }} {{ checked }}</label>
  </div>
</template>

<script>
    export default {
        data() {
            return {

            }
        },
        props: ['label', 'checked', 'id']
    }
</script>

<style>
    .field {
        /* background: grey; */
    }
</style>
