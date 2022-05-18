<template>
  <v-row justify="center" align="center">
    <v-col cols="12">
      <v-data-table
        :headers="categoriesHeaders"
        :items="categoriesData.body"
        class="elevation-1"
      ></v-data-table>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'CategoriesPage',
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
