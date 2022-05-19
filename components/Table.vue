<template>
  <v-data-table :headers="headers" :items="items" class="elevation-1">
  </v-data-table>
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
  },
}
</script>
