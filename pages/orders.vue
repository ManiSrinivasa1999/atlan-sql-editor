<template>
  <v-row justify="center" align="center">
    <v-col cols="12">
      <v-data-table
        :headers="ordersHeaders"
        :items="ordersData.body"
        class="elevation-1"
      ></v-data-table>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'OrdersPage',
  async asyncData({ $content, params, error }) {
    const slug = params.slug || 'csv/orders'
    const ordersData = await $content(slug)
      .fetch()
      .catch((_err) => {
        error({ statusCode: 404, message: 'Page not found' })
      })
    return {
      ordersData,
    }
  },
  data() {
    return {
      ordersHeaders: [
        { text: 'Order ID', value: 'orderID' },
        { text: 'Customer ID', value: 'customerID' },
        { text: 'Employee ID', value: 'employeeID' },
        { text: 'Order Date', value: 'orderDate' },
        { text: 'Required Date', value: 'requiredDate' },
        { text: 'Shipped Date', value: 'shippedDate' },
        { text: 'Ship Via', value: 'shipVia' },
        { text: 'Freight', value: 'freight' },
        { text: 'Ship Name', value: 'shipName' },
        { text: 'Ship Address', value: 'shipAddress' },
        { text: 'Ship City', value: 'shipCity' },
        { text: 'Ship Region', value: 'shipRegion' },
        { text: 'Ship Postal Code', value: 'shipPostalCode' },
        { text: 'Ship Country', value: 'shipCountry' },
      ],
    }
  },
}
</script>
