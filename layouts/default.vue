<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-btn icon @click.stop="miniVariant = !miniVariant">
        <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>
      <v-btn icon @click.stop="clipped = !clipped">
        <v-icon>mdi-application</v-icon>
      </v-btn>
      <v-spacer />
      <v-toolbar-title
        class="font-weight-bold text-h4 text-primary"
        v-text="title"
      />
      <v-spacer />
      <v-btn icon @click="$vuetify.theme.dark = !$vuetify.theme.dark"
        ><v-icon> mdi-theme-light-dark </v-icon></v-btn
      >
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer app class="text-center">
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-home',
          title: 'Home',
          to: '/',
        },
        {
          icon: 'mdi-apps',
          title: 'Categories',
          to: '/categories',
        },
        {
          icon: 'mdi-account-group',
          title: 'Customers',
          to: '/customers',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Employee Territories',
          to: '/employee-territories',
        },
        {
          icon: 'mdi-account-group',
          title: 'Employees',
          to: '/employees',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Order Details',
          to: '/order-details',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Orders',
          to: '/orders',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Products',
          to: '/products',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Regions',
          to: '/regions',
        },
        {
          icon: 'mdi-account-group',
          title: 'Shippers',
          to: '/shippers',
        },
        {
          icon: 'mdi-account-group',
          title: 'Suppliers',
          to: '/suppliers',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Territories',
          to: '/territories',
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Sql Queries',
    }
  },
}
</script>
