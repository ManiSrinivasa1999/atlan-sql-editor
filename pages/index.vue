<template>
  <v-container>
    <v-row align="center" justify="center">
      <v-col cols="2" class="text-h6 word-spacing pr-0"> Select * from </v-col>
      <v-col cols="2">
        <v-select
          v-model="selectedTable"
          :items="Object.keys(tablesList)"
          label="Select Table"
          @change="displayTable()"
        ></v-select>
      </v-col>
    </v-row>
    <v-row align="center" justify="center">
      <Table v-if="isSelected" :headers="headers" :items="items.body" />
    </v-row>
  </v-container>
</template>

<script>
import Table from '~/components/Table.vue'
export default {
  name: 'IndexPage',
  components: { Table },
  data() {
    return {
      selectedTable: '',
      isSelected: false,
      tablesList: {
        Categories: 'categories',
        Customers: 'customers',
        EmployeeTerritories: 'employee_territories',
        Employees: 'employees',
        OrderDetails: 'order_details',
        Orders: 'orders',
        Products: 'products',
        Regions: 'regions',
        Shippers: 'shippers',
        Suppliers: 'suppliers',
        Territories: 'territories',
      },
      headers: [],
      items: [],
    }
  },
  methods: {
    async displayTable() {
      const slug = this.tablesList[this.selectedTable]
      try {
        this.items = await this.$content(`csv/${slug}`).fetch()
        this.isSelected = true
      } catch (error) {
        error({ statusCode: 404, message: 'Page not found' })
      }
    },
  },
}
</script>
<style scoped>
.word-spacing {
  word-spacing: 2vw;
}
</style>