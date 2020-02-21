<template>
  <v-row>
    <v-col sm="3">
      <v-card>
        <v-card-title>Calculate Profit</v-card-title>
        <v-card-text>
          <v-text-field
            v-model="CDData.Amount"
            prefix="$"
            label="Amount"
            placeholder="1000.00"
          />
          <v-text-field
            v-model="CDData.Rate"
            label="Rate"
            placeholder="1.5"
            append-icon="%"
          />
          <v-select
            v-model="CDData.Period"
            class="my-2"
            :items="dropdown_period"
            label="Period"
          />
          <v-btn color="primary" @click="GetProfit">
            Result
          </v-btn>
          <v-text-field v-model="CDData.Profit" prefix="$" label="Profit" placeholder="0" readonly />
        </v-card-text>
      </v-card>
    </v-col>
    <v-col sm="3">
      <v-card>
        <v-card-title>Calculate Amount</v-card-title>
        <v-card-text>
          <v-text-field
            v-model="CDDataReverse.Profit"
            prefix="$"
            label="Profit"
            placeholder="2.00"
          />
          <v-text-field
            v-model="CDDataReverse.Rate"
            label="Rate"
            placeholder="1.5"
            append-icon="%"
          />
          <v-select
            v-model="CDDataReverse.Period"
            class="my-2"
            :items="dropdown_period"
            label="Period"
          />
          <v-btn color="primary" @click="GetAmount">
            Result
          </v-btn>
          <v-text-field v-model="CDDataReverse.Amount" prefix="$" label="Amount" placeholder="0" readonly />
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data: () => ({
    dropdown_period: ['One Month', 'Three Months', 'Six Months', 'A Year'],
    month_period: [1, 3, 6, 12],
    CDData: { Amount: 0, Rate: 0, Period: 'One Month', Profit: 0 },
    CDDataReverse: { Amount: 0, Rate: 0, Period: 'One Month', Profit: 0 }
  }),
  methods: {
    /**
     * @return {number}
     */
    GetPeriod (Period) {
      return this.month_period[this.dropdown_period.indexOf(Period)]
    },
    GetProfit () {
      const profit = this.CDData.Amount * this.CDData.Rate / 100 / 12 * this.GetPeriod(this.CDData.Period)
      this.CDData.Profit = profit.toFixed(2)
    },
    GetAmount () {
      const amount = this.CDDataReverse.Profit * 12 * 100 / this.GetPeriod(this.CDDataReverse.Period) / this.CDDataReverse.Rate
      this.CDDataReverse.Amount = amount.toFixed(2)
    }
  }
}
</script>
