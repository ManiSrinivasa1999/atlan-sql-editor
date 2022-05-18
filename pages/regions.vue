<template>
  <v-row justify="center" align="center">
    <v-col cols="12">
      <v-data-table
        :headers="regionsHeaders"
        :items="regionsData.body"
        class="elevation-1"
      ></v-data-table>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'RegionsPage',
  async asyncData({ $content, params, error }) {
    const slug = params.slug || 'csv/regions'
    const regionsData = await $content(slug)
      .fetch()
      .catch((_err) => {
        error({ statusCode: 404, message: 'Page not found' })
      })
    return {
      regionsData,
    }
  },
  data() {
    return {
      regionsHeaders: [
        { text: 'Region ID', value: 'regionID' },
        { text: 'Region Description', value: 'regionDescription' },
      ],
    }
  },
}
</script>
