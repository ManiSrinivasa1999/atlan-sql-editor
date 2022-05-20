<template>
  <v-container>
    <v-row justify="center" class="mt-2">
      <v-col cols="12" md="2" class="text-prop pr-0"> Select * from </v-col>
      <v-col cols="12" md="2" class="pl-0">
        <v-select
          v-model="selectedTable"
          :items="Object.keys(tablesList)"
          label="Select Table"
          background-color="primary"
          item-color="secondary"
          solo
          @change="displayTable()"
        ></v-select>
      </v-col>
    </v-row>
    <v-row v-if="true" align="center" justify="center">
      <Table
        v-if="isSelected"
        :headers="headers"
        :items="items.body"
        :loading="loading"
      />
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
      selectedTable: 'customers',
      isSelected: false,
      loading: false,
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
  mounted() {},
  methods: {
    async displayTable() {
      this.loading = true
      const slug = this.tablesList[this.selectedTable]
      try {
        this.items = await this.$content(`csv/${slug}`).fetch()
        const jsonData = await this.$content('json/header').fetch()
        this.headers = jsonData[this.selectedTable]
        // console.log(this.items)
      } catch (error) {
        error({ statusCode: 404, message: 'Page not found' })
      } finally {
        this.isSelected = true
        this.loading = false
      }
    },
  },
}
</script>
<style lang="scss" scoped>
.text-prop {
  word-spacing: 1vw;
  font-size: 36px;
  font-weight: 500;
}
</style>