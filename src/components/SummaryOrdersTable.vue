<template>
  <div>
    <h2>סיכום הזמנות</h2>
    <SummaryTable :tableData="tableData" />
  </div>
</template>

<script>
import SummaryTable from '@/components/SummaryTable'

export default {
  name: 'SummaryOrdersTable',
  components: {
    SummaryTable
  },
  props: {
    orders: Array,
  },
  created() {
    // Init summary table data using the correct data structure
    setTimeout(() => {
      this.updateTableData()
    }, 50);
  },
  // Update summary table data using the correct data structure
  updated() {
    setTimeout(() => {
      this.updateTableData()
    }, 50);
  },
  data: () => ({
    tableData: [
      {
        title: 'כמות הזמנות',
        val: ''
      },
      {
        title: 'סה"כ עלות הזמנות',
        val: ''
      },
      {
        title: 'ממוצע עלות משלוחים',
        val: ''
      }
    ],
  }),
  methods: {
    // Quantity of orders
    getQuantityOfOrders() {
      return this.orders.length
    },
    // Total cost of orders(sum function)
    getTotalCostOfOrders() {
      var totalCost = 0
      for (let i = 0; i < this.orders.length; i++) {
        totalCost += Number(this.orders[i]['shippingCost'])
      }
      return Number(totalCost).toFixed(2)
    },
    // Average order cost
    getAvgOrderCost() {
      return Number(Number(this.getTotalCostOfOrders()) / Number(this.getQuantityOfOrders())).toFixed(2)
    },
    // update summary table with new values using the correct data structure
    updateTableData() {
      this.tableData = [
        {
          title: 'כמות הזמנות',
          val: this.getQuantityOfOrders()
        },
        {
          title: 'סה"כ עלות הזמנות',
          val: this.getTotalCostOfOrders()
        },
        {
          title: 'ממוצע עלות משלוח',
          val: this.getAvgOrderCost()
        }
      ]
    }
  }
  
}
</script>

