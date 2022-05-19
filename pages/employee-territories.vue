<template>
  <Table
    :headers="employeeTerritoriesHeaders"
    :items="employeeTerritoriesData.body"
  />
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
