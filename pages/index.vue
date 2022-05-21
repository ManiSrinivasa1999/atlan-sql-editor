<template>
  <v-container>
    <v-row v-if="$vuetify.breakpoint.mdAndUp" justify="center" class="mt-2">
      <v-col cols="12" xl="2" lg="3" md="4" class="text-prop pr-0">
        Select * from
      </v-col>
      <v-col cols="12" xl="2" lg="3" md="4" class="pl-0">
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
    <v-row v-if="$vuetify.breakpoint.mdAndUp" align="center" justify="center">
      <Table
        v-if="isSelected"
        :headers="headers"
        :items="items"
        :loading="loading"
      />
    </v-row>
    <v-row
      v-if="$vuetify.breakpoint.smAndDown"
      justify="center"
      class="mt-2 text-h4 font-weignt-bold"
    >
      Coming soon...
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
        this.items = []
        const data = await this.$content(`csv/${slug}`).fetch()
        const jsonData = await this.$content('json/header').fetch()
        this.headers = jsonData[this.selectedTable]
        if (this.headers[this.headers.length - 1].value === 'picture') {
          for (let index = 0; index < data.body.length; index += 1) {
            this.items.push({
              categoryID: data.body[index].categoryID,
              categoryName: data.body[index].categoryName,
              description: data.body[index].description,
              picture: data.body[index].picture.slice(0, 20),
            })
          }
        } else if (this.headers[this.headers.length - 1].value === 'photo') {
          for (let index = 0; index < data.body.length; index += 1) {
            this.items.push({
              employeeID: data.body[index].employeeID,
              lastName: data.body[index].lastName,
              firstName: data.body[index].firstName,
              title: data.body[index].title,
              titleOfCourtesy: data.body[index].titleOfCourtesy,
              birthDate: data.body[index].birthDate,
              hireDate: data.body[index].hireDate,
              address: data.body[index].address,
              city: data.body[index].city,
              region: data.body[index].region,
              postalCode: data.body[index].postalCode,
              country: data.body[index].country,
              homePhone: data.body[index].homePhone,
              extension: data.body[index].extension,
              notes: data.body[index].notes.slice(0, 20),
              reportsTo: data.body[index].reportsTo,
              photoPath: data.body[index].photoPath.slice(0, 10),
              photo: data.body[index].photo.slice(0, 10),
            })
          }
        } else {
          this.items = data.body
        }
      } catch (error) {
        error({ statusCode: 404, message: 'Page not found' })
      } finally {
        this.isSelected = true
        this.loading = false
      }
    },
    // async innerJoin() {
    //   this.loading = true
    //   const results = []
    //   const tableOne = await this.$content(`csv/employee_territories`).fetch()
    //   const tableTwo = await this.$content(`csv/employees`).fetch()
    //   // const jsonData = await this.$content('json/header').fetch()
    //   // debugger
    //   const tableOneBody = tableOne.body
    //   const tableTwoBody = tableTwo.body
    //   this.headers = [
    //     { text: 'Employee ID', value: 'employeeID' },
    //     { text: 'Last name', value: 'lastName' },
    //     { text: 'First name', value: 'firstName' },
    //     { text: 'Title', value: 'title' },
    //     { text: 'Title of courtesy', value: 'titleOfCourtesy' },
    //     { text: 'Birth date', value: 'birthDate' },
    //     { text: 'Hire date', value: 'hireDate' },
    //     { text: 'Address', value: 'address' },
    //     { text: 'City', value: 'city' },
    //     { text: 'Region', value: 'region' },
    //     { text: 'Postal code', value: 'postalCode' },
    //     { text: 'Country', value: 'country' },
    //     { text: 'Home phone', value: 'homePhone' },
    //     { text: 'Extension', value: 'extension' },
    //     { text: 'Photo', value: 'photo' },
    //     { text: 'Notes', value: 'notes' },
    //     { text: 'Reports to', value: 'reportsTo' },
    //     { text: 'Photo path', value: 'photoPath' },
    //     { text: 'Territory Name', value: 'territoryID' },
    //   ]
    //   for (let i = 0; i < tableOneBody.length; i++) {
    //     for (let j = 0; j < tableTwoBody.length; j++) {
    //       if (tableOneBody[i].employeeID === tableTwoBody[j].employeeID) {
    //         results.push({
    //           employeeID: tableTwoBody[i].employeeID,
    //           lastName: tableTwoBody[i].lastName,
    //           firstName: tableTwoBody[i].firstName,
    //           title: tableTwoBody[i].title,
    //           titleOfCourtesy: tableTwoBody[i].titleOfCourtesy,
    //           birthDate: tableTwoBody[i].birthDate,
    //           hireDate: tableTwoBody[i].hireDate,
    //           address: tableTwoBody[i].address,
    //           city: tableTwoBody[i].city,
    //           region: tableTwoBody[i].region,
    //           postalCode: tableTwoBody[i].postalCode,
    //           country: tableTwoBody[i].country,
    //           homePhone: tableTwoBody[i].homePhone,
    //           extension: tableTwoBody[i].extension,
    //           photo: tableTwoBody[i].photo,
    //           notes: tableTwoBody[i].notes,
    //           reportsTo: tableTwoBody[i].reportsTo,
    //           photoPath: tableTwoBody[i].photoPath,
    //           territoryID: tableOneBody[i].territoryID,
    //         })
    //       }
    //     }
    //   }
    //   this.isSelected = true
    //   this.loading = false
    //   this.items = results
    // },
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