<template>
  <Table :headers="customersHeaders" :items="customersData.body" />
</template>

<script>
export default {
  name: 'CustomersPage',
  async asyncData({ $content, params, error }) {
    const slug = params.slug || 'csv/customers'
    const customersData = await $content(slug)
      .fetch()
      .catch((_err) => {
        error({ statusCode: 404, message: 'Page not found' })
      })
    return {
      customersData,
    }
  },
  data() {
    return {
      customersHeaders: [
        { text: 'Customer ID', value: 'customerID' },
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
      ],
    }
  },
}
</script>
