<template>
  <div class="body">
    <div id="app" class="bill">
      <div class="brand">Al-Shaikh Pharmacy</div>
      <div style="margin-top: 3px" class="address">
        Noor Shah Chowk Kot Addu
      </div>
      <div style="margin-top: 3px">INVOICE</div>
      <div style="margin-top: 3px" class="bill-details">
        <div class="flex justify-between">
          <div>BILL NO: 213</div>
        </div>
        <div style="margin-top: 2px" class="flex justify-between">
          <div>BILL DATE: 10/05/2024</div>
          <div>TIME: 16:21</div>
        </div>
      </div>

      <table class="table">
        <!-- Header row -->
        <tr class="header">
          <th>Particulars</th>
          <th>Rate</th>
          <th>Qty</th>
          <th>Amount</th>
        </tr>

        <!-- Medicine rows with v-for loop -->
        <tr v-for="(medicine, index) in medicines" :key="index">
          <td>{{ medicine.name }}</td>
          <td>{{ medicine.rate }}</td>
          <td>{{ medicine.quantity }}</td>
          <td>{{ calculateAmount(medicine) }}</td>
        </tr>

        <!-- Total row -->
        <tr class="total">
          <td></td>
          <td>Total</td>
          <td></td>
          <td>{{ total }}</td>
        </tr>

        <!-- Discount row -->
        <tr>
          <td></td>
          <td>Discount</td>
          <td></td>
          <td>{{ discount }}</td>
        </tr>

        <!-- Net Amount row -->
        <tr class="net-amount">
          <td></td>
          <td>Net Amnt</td>
          <td></td>
          <td>{{ netAmount }}</td>
        </tr>
      </table>
      <div style="margin-top: 5px">Thank You! Please Visit Again</div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const medicines = ref([
  { name: "ITP OD 150 mg Tab", rate: 46, quantity: 20 },
  { name: "Emildap 10 mg Tab", rate: 235, quantity: 10 },
  { name: "Evion 400 mg Caps", rate: 26, quantity: 20 },
  { name: "Myteka 10 mg Tab", rate: 223, quantity: 10 },
  { name: "Vom 20 mg Tablet", rate: 46, quantity: 20 },
  { name: "Nebi 2.5 mg Tab", rate: 152, quantity: 10 },
  { name: "Alp 0.25 mg Tab", rate: 26, quantity: 15 },
  { name: "Syp Lagita advance", rate: 143, quantity: 8 },
]);

const calculateAmount = (medicine) => {
  return medicine.rate * medicine.quantity;
};

const total = computed(() => {
  return medicines.value.reduce(
    (acc, medicine) => acc + calculateAmount(medicine),
    0
  );
});

const discount = computed(() => {
  return Math.floor(total.value * 0.05); // Rounded down to the nearest whole number
});

const netAmount = computed(() => {
  return total.value - discount.value;
});
</script>

<style scoped>
@import url("http://fonts.cdnfonts.com/css/vcr-osd-mono");
.body {
  color: black;
  text-align: center;
  display: flex;
  justify-content: center;
  font-size: 20px;
}
.bill {
  margin-top: 5%;
  width: 400px;
  box-shadow: 0 0 3px #aaa;
  padding: 10px 10px;
  box-sizing: border-box;
}
.flex {
  display: flex;
}
.justify-between {
  justify-content: space-between;
}
.table {
  border-collapse: collapse;
  width: 100%;
}
.table .header {
  border-top: 2px dashed #000;
  border-bottom: 2px dashed #000;
}
.table {
  text-align: left;
}
.table .total td:first-of-type {
  border-top: none;
  border-bottom: none;
}
.table .total td {
  border-top: 2px dashed #000;
  border-bottom: 2px dashed #000;
}
.table .net-amount td:first-of-type {
  border-top: none;
}
.table .net-amount td {
  border-top: 2px dashed #000;
}
.table .net-amount {
  border-bottom: 2px dashed #000;
}
@media print {
  .hidden-print,
  .hidden-print * {
    display: none !important;
  }
}
</style>
