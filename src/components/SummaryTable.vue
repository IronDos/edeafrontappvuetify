<template>
  <div>
    <v-simple-table style="width:100%">
      <template v-slot:default class="p0 m0" style="width:100%">
        <tbody>
          <tr
          v-for="(tdata) in tableData"
          :key="tdata.title"
          >
            <td class="tdtitle text-center">{{ tdata.title }}</td>
            <td class="text-center">{{ tdata.val }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </div>
</template>

<script>
export default {
  name: 'SummaryTable',
  props: {
    tableData: Array,
  }
}
</script>

<style scoped>
.tdtitle {
  background-color: #D0D0D0;
}
</style>

