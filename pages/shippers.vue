<template>
  <Table :headers="shippersHeaders" :items="shippersData.body" />
</template>

<script>
export default {
  name: 'ShippersPage',
  async asyncData({ $content, params, error }) {
    const slug = params.slug || 'csv/shippers'
    const shippersData = await $content(slug)
      .fetch()
      .catch((_err) => {
        error({ statusCode: 404, message: 'Page not found' })
      })
    return {
      shippersData,
    }
  },
  data() {
    return {
      shippersHeaders: [
        { text: 'Shipper ID', value: 'shipperID' },
        { text: 'Company Name', value: 'companyName' },
        { text: 'Phone', value: 'phone' },
      ],
    }
  },
}
</script>
