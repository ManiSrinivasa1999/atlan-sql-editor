<template>
  <v-card v-if="$vuetify.breakpoint.mdAndUp" color="primary">
    <v-card-text>
      <v-container>
        <v-data-table
          dark
          :headers="headers"
          :items="items"
          :loading="loading"
          loading-text="Loading data..."
          class="st-color"
        >
        </v-data-table></v-container></v-card-text
  ></v-card>
</template>

<script>
export default {
  name: 'TableComponent',
  props: {
    items: {
      type: Array,
      required: true,
    },
    headers: {
      type: Array,
      required: true,
    },
    loading: {
      type: Boolean,
      default: true,
    },
  },
}
</script>
<style>
.truncate {
  display: inline-block;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.st-color {
  background-color: #10163a !important;
}
</style>
