<template>
  <Table :headers="regionsHeaders" :items="regionsData.body" />
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
