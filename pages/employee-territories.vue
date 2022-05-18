<template>
  <v-row justify="center" align="center">
    <v-col cols="12">
      <v-data-table
        :headers="employeeTerritoriesHeaders"
        :items="employeeTerritoriesData.body"
        class="elevation-1"
      ></v-data-table>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'EmployeeTerritoriesPage',
  async asyncData({ $content, params, error }) {
    const slug = params.slug || 'csv/employee_territories'
    const employeeTerritoriesData = await $content(slug)
      .fetch()
      .catch((_err) => {
        error({ statusCode: 404, message: 'Page not found' })
      })
    return {
      employeeTerritoriesData,
    }
  },
  data() {
    return {
      employeeTerritoriesHeaders: [
        { text: 'Employee ID', value: 'employeeID' },
        { text: 'Territory Name', value: 'territoryID' },
      ],
    }
  },
}
</script>
