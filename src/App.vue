<template>
  <div id="app">
    <DatasetSchemaOrgMarkup doi="10.25677/10968/570"/>
  </div>
</template>

<script>
import DatasetSchemaOrgMarkup from './components/DatasetSchemaOrgMarkup.vue'
import axios from 'axios';

export default {
  name: 'app',
  components: {
    DatasetSchemaOrgMarkup
  }
}
</script>

<style>
#app {
}
</style>
