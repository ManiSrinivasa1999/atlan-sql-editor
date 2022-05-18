<template>
  <v-row justify="center" align="center">
    <v-col cols="12">
      <v-data-table
        :headers="employeesHeaders"
        :items="employeesData.body"
        class="elevation-1"
      ></v-data-table>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'EmployeesPage',
  async asyncData({ $content, params, error }) {
    const slug = params.slug || 'csv/employees'
    const employeesData = await $content(slug)
      .fetch()
      .catch((_err) => {
        error({ statusCode: 404, message: 'Page not found' })
      })
    return {
      employeesData,
    }
  },
  data() {
    return {
      employeesHeaders: [
        { text: 'Employee id', value: 'employeeID' },
        { text: 'Last name', value: 'lastName' },
        { text: 'First name', value: 'firstName' },
        { text: 'Title', value: 'title' },
        { text: 'Title of courtesy', value: 'titleOfCourtesy' },
        { text: 'Birth date', value: 'birthDate' },
        { text: 'Hire date', value: 'hireDate' },
        { text: 'Address', value: 'address' },
        { text: 'City', value: 'city' },
        { text: 'Region', value: 'region' },
        { text: 'Postal code', value: 'postalCode' },
        { text: 'Country', value: 'country' },
        { text: 'Home phone', value: 'homePhone' },
        { text: 'Extension', value: 'extension' },
        { text: 'Photo', value: 'photo' },
        { text: 'Notes', value: 'notes' },
        { text: 'Reports to', value: 'reportsTo' },
        { text: 'Photo path', value: 'photoPath' },
      ],
    }
  },
}
</script>
