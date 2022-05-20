<template>
  <v-app class="bg-color" dark>
    <v-main>
      <v-container fluid>
        <v-card color="primary">
          <v-container class="d-flex justify-center align-center" fluid>
            <v-btn to="/" color="secondary" dark>
              <span> {{ title }} </span>
            </v-btn>
          </v-container>
        </v-card>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      title: 'Sql Queries',
    }
  },
}
</script>
<style lang="scss" scoped>
.bg-color {
  background-color: #262c49 !important;
}
</style>
