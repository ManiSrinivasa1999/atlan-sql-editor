<template>
  <Table :headers="territoriesHeaders" :items="territoriesData.body" />
</template>

<script>
export default {
  name: 'TerritoriesPage',
  async asyncData({ $content, params, error }) {
    const slug = params.slug || 'csv/territories'
    const territoriesData = await $content(slug)
      .fetch()
      .catch((_err) => {
        error({ statusCode: 404, message: 'Page not found' })
      })
    return {
      territoriesData,
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
