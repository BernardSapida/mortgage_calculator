<template>
  <div class="main_container p-3 rounded">
    <div class="form_container p-5 rounded">
      <h1 class="mb-5"><strong>Mortage Calculator</strong></h1>
      <form @submit.prevent>
        <div class="row">
          <div class="col-4 mb-3">
            <label for="purchase_price" class="form-label">Purchase price: <strong>${{computed_purchase_price}}</strong></label>
            <input type="range" class="form-range" min="0" max="1000000" step="1000" id="purchase_price" v-model="purchase_price">
          </div>
          <div class="col-4 mb-3">
            <label for="down_payment" class="form-label">Down payment: <strong>${{computed_down_payment}}</strong></label>
            <input type="range" class="form-range" min="0" max="1000000" step="1000" id="down_payment" v-model="down_payment">
          </div>
          <div class="col-4 mb-3">
            <label for="repayment_time" class="form-label">Repayment time: <strong>{{repayment_time}} years</strong></label>
            <input type="range" class="form-range" min="1" max="30" step="1" id="repayment_time" v-model="repayment_time">
          </div>
          <div class="col-4 mb-3">
            <label for="interest_rate" class="form-label">Interest rate: <strong>{{interest_rate}}%</strong></label>
            <input type="range" class="form-range" min="0" max="100" step="0.5" id="interest_rate" v-model="interest_rate">
          </div>
          <div class="col-4 mb-3">
            <p>Loan Amount</p>
            <h3><strong>${{computed_loan_amount}}</strong></h3>
          </div>
          <div class="col-4 mb-3">
            <p>Estimated per month</p>
            <h3><strong>${{computed_monthly_mortgage}}</strong></h3>
          </div>
        </div>
        <button type="submit" class="btn btn-primary py-3 px-5" @click="calculateMortgage">Get a mortgage quote</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MainPage',
  props: {
    msg: String
  },
  data() {
    return {
      purchase_price: 0,
      down_payment: 0,
      repayment_time: 0,
      interest_rate: 0,
      loan_amount: 0,
      monthly_mortgage: 0
    }
  },
  computed: {
    computed_purchase_price() {
      return this.purchase_price.toFixed(2).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
    computed_down_payment() {
      return this.down_payment.toFixed(2).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
    computed_loan_amount() {
      return this.loan_amount.toFixed(2).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
    computed_monthly_mortgage() {
      return this.monthly_mortgage.toFixed(2).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    }
  },
  methods: {
    calculateMortgage() {
      let { purchase_price, down_payment, repayment_time, interest_rate } = this;
      let rate = interest_rate/100;
      let time_period = repayment_time*12;

      this.loan_amount = purchase_price - down_payment;
      this.monthly_mortgage = this.loan_amount * rate * (1 + rate)**time_period / ((1 + rate)**time_period - 1);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  @import url("../../public/css/index.css");
</style>
