<template>
  <Table :headers="orderDetailsHeaders" :items="orderDetailsData.body" />
</template>

<script>
export default {
  name: 'OrderDeatilsPage',
  async asyncData({ $content, params, error }) {
    const slug = params.slug || 'csv/order_details'
    const orderDetailsData = await $content(slug)
      .fetch()
      .catch((_err) => {
        error({ statusCode: 404, message: 'Page not found' })
      })
    return {
      orderDetailsData,
    }
  },
  data() {
    return {
      orderDetailsHeaders: [
        { text: 'Order ID', value: 'orderID' },
        { text: 'Product ID', value: 'productID' },
        { text: 'Unit Price', value: 'unitPrice' },
        { text: 'Quantity', value: 'quantity' },
        { text: 'Discount', value: 'discount' },
      ],
    }
  },
}
</script>
