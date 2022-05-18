<template>
  <v-row justify="center" align="center">
    <v-col cols="12">
      <v-data-table
        :headers="territoriesHeaders"
        :items="categoriesData.body"
        class="elevation-1"
      ></v-data-table>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'TerritoriesPage',
  async asyncData({ $content, params, error }) {
    const slug = params.slug || 'csv/territories'
    const categoriesData = await $content(slug)
      .fetch()
      .catch((_err) => {
        error({ statusCode: 404, message: 'Page not found' })
      })
    return {
      categoriesData,
    }
  },
  data() {
    return {
      territoriesHeaders: [
        { text: 'Territory ID', value: 'territoryID' },
        { text: 'Territory Description', value: 'territoryDescription' },
        { text: 'Region ID', value: 'regionID' },
      ],
    }
  },
}
</script>
