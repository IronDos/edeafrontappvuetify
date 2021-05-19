<template>
  <div>
    <h2>הזמנות אחרונות</h2>
    <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-center">
            מזהה הזמנה
          </th>
          <th class="text-center">
            שם לקוח
          </th>
          <th v-if="mobile == false" class="text-center">
            כתובת משלוח
          </th>
          <th v-if="mobile == false" class="text-center">
            עיר משלוח
          </th>
          <th v-if="mobile == false" class="text-center">
            אזור משלוח
          </th>
          <th  class="text-center">
            עלות משלוח
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(order,index) in orders"
          :key="order.id"
          v-bind:style="[index % 2 != 0 ? {'background-color': '#D0D0D0'} : {}]"
          class="text-center"
        >
          <td>{{ order.id }}</td>
          <td class="pa-0">
            <input type="text" maxlength="30" v-model="order.customerCompanyName">
          </td>
          <td v-if="mobile == false">{{ order.address }}</td>
          <td v-if="mobile == false">{{ order.city }}</td>
          <td v-if="mobile == false">{{ order.region }}</td>
          <td class="pa-0">
            <input type="number" min="0" @input="fixTwo(index)" v-model="order.shippingCost">
          </td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
  </div>
</template>

<script>
export default {
  name: 'OrdersTable',
  props: {
    orders: Array,
  },
  mounted(){
    // listen to screen size
    addEventListener('resize', () => {
      this.mobile = innerWidth <= 300
    })
  },
  data: () => ({
    mobile: window.innerWidth <= 300
  }),
  methods: {
    // 2 digits after point .xx
    fixTwo(index) {
      this.orders[index]['shippingCost'] = Number(this.orders[index]['shippingCost']).toFixed(2)
    }
  }
}
</script>

<style scoped>
thead {
  background-color: #EBFF89;
}

tbody tr:hover {
  background-color: #90EE90 !important;
}
input {
  height: 100%;
  width: 100%;
  text-align:center;
}
</style>