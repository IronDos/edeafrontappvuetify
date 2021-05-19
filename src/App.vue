<template>
  <v-app>
    <h1 class="text-center">Edea Dashboard</h1>
    <v-main>
      <v-row>
        <v-col
        cols="12" xs="12" sm="8" md="8" lg="10" xl="10" order-xs="1" order-sm="2" order-md="2" order-lg="2"
        class="p0 m0">
          <OrdersTable :orders="orders" />
        </v-col>
        <v-col
        cols="12" xs="12" sm="4" md="4" lg="2" xl="2" order-xs="-1" order-sm="1" order-md="1" order-lg="1"
        class="p0 m0">
          <SummaryOrdersTable :orders="orders" />
        </v-col>
        
      </v-row>
    </v-main>
  </v-app>
</template>

<script>
import OrdersTable from '@/components/OrdersTable';
import SummaryOrdersTable from '@/components/SummaryOrdersTable';

import axios from 'axios'

export default {
  name: 'App',
  components: {
    OrdersTable,
    SummaryOrdersTable
  },

  data: () => ({
    orders: [],
    customers: []
  }),
  
  created () {
    this.getAllCustomers()
  },

  methods: {
    // get req all orders collection
    getAllOrders() {
      axios
      .get('api/orders')
      .then(response => {
        this.orders = response["data"]
        this.setupCompanyName()
      })
      .catch(() => (console.log("Orders API Error")))      
    },
    // get req all customer collection
    getAllCustomers() {
      axios
      .get('api/customers')
      .then(response => {
        this.customers = response["data"]
        this.getAllOrders()
      })
      .catch(() => (console.log("Customers API Error")))
    },
    // set company name for each order
    setupCompanyName() {
      for (let i = 0; i < this.orders.length; i++) {
        for (let j = 0; j < this.customers.length; j++) {
          if (this.orders[i]['customerId'] == this.customers[j]['id']) {
            this.orders[i]['customerCompanyName'] = this.customers[j]['companyName']
            break
          }
        }
      }
    }
  }
}
</script>
