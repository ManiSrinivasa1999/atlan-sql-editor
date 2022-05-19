<template>
  <Table :headers="productsHeaders" :items="productsData.body" />
</template>

<script>
export default {
  name: 'ProductsPage',
  async asyncData({ $content, params, error }) {
    const slug = params.slug || 'csv/products'
    const productsData = await $content(slug)
      .fetch()
      .catch((_err) => {
        error({ statusCode: 404, message: 'Page not found' })
      })
    return {
      productsData,
    }
  },
  data() {
    return {
      productsHeaders: [
        { text: 'Product ID', value: 'productID' },
        { text: 'Product Name', value: 'productName' },
        { text: 'Supplier ID', value: 'supplierID' },
        { text: 'Category ID', value: 'categoryID' },
        { text: 'Quantity Per Unit', value: 'quantityPerUnit' },
        { text: 'Unit Price', value: 'unitPrice' },
        { text: 'Units In Stock', value: 'unitsInStock' },
        { text: 'Units On Order', value: 'unitsOnOrder' },
        { text: 'Reorder Level', value: 'reorderLevel' },
        { text: 'Riscontinued', value: 'discontinued' },
      ],
    }
  },
}
</script>
