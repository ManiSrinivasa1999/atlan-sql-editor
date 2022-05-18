<template>
  <v-row justify="center" align="center">
    <v-col cols="12">
      <v-data-table
        :headers="shippersHeaders"
        :items="shippersData.body"
        class="elevation-1"
      ></v-data-table>
    </v-col>
  </v-row>
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
