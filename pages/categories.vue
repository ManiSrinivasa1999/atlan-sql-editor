<template>
  <Table :headers="categoriesHeaders" :items="categoriesData.body" />
</template>

<script>
import Table from '../components/Table.vue'
export default {
  name: 'CategoriesPage',
  components: {
    Table,
  },
  async asyncData({ $content, params, error }) {
    const slug = params.slug || 'csv/categories'
    const categoriesData = await $content(slug)
      .fetch()
      .catch((_err) => {
        error({ statusCode: 404, message: 'Page not found' })
      })
    return {
      categoriesData,
    }
  },
  data() {
    return {
      categoriesHeaders: [
        { text: 'Category ID', value: 'categoryID' },
        { text: 'Category Name', value: 'categoryName' },
        { text: 'Description', value: 'description' },
        { text: 'Picture', value: 'picture' },
      ],
    }
  },
}
</script>
