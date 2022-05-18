<template>
  <v-row justify="center" align="center">
    <v-col cols="12">
      <v-data-table
        :headers="suppliersHeaders"
        :items="suppliersData.body"
        class="elevation-1"
      ></v-data-table>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'SuppliersPage',
  async asyncData({ $content, params, error }) {
    const slug = params.slug || 'csv/suppliers'
    const suppliersData = await $content(slug)
      .fetch()
      .catch((_err) => {
        error({ statusCode: 404, message: 'Page not found' })
      })
    return {
      suppliersData,
    }
  },
  data() {
    return {
      suppliersHeaders: [
        { text: 'Supplier ID', value: 'supplierID' },
        { text: 'Company Name', value: 'companyName' },
        { text: 'Contact Name', value: 'contactName' },
        { text: 'Contact Title', value: 'contactTitle' },
        { text: 'Address', value: 'address' },
        { text: 'City', value: 'city' },
        { text: 'Region', value: 'region' },
        { text: 'Postal Code', value: 'postalCode' },
        { text: 'Country', value: 'country' },
        { text: 'Phone', value: 'phone' },
        { text: 'Fax', value: 'fax' },
        { text: 'Home Page', value: 'homePage' },
      ],
    }
  },
}
</script>
