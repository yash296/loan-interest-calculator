<template>
  <div>
    <v-container>
      <v-row>
        <v-col class="pa-4" cols="12" sm="6">
          <v-card class="pa-4" outlined width="100%">
            <div class="text-center">Interest Rate</div>
            {{cacheItem.interestRate}}
          </v-card>
        </v-col>
        <v-col class="pa-4" cols="12" sm="6">
          <v-card class="pa-4" outlined width="100%">
            <div class="text-center">Monthly Payment</div>
            {{cacheItem.monthlyPayment.amount}} {{cacheItem.monthlyPayment.currency}}
          </v-card>
        </v-col>
        <v-col class="pa-4" cols="12" sm="6">
          <v-card class="pa-4" outlined width="100%">
            <div class="text-center">Number Of Payments</div>
            {{cacheItem.numPayments}}
          </v-card>
        </v-col>
        <v-col class="pa-4" cols="12" sm="6">
          <v-card class="pa-4" outlined width="100%">
            <div class="text-center">Principal</div>
            {{cacheItem.principal.amount}} {{cacheItem.principal.currency}}
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>
<script>
export default {
  props: {
    cacheItem: {
      type: Object,
      default() {
        return {};
      }
    }
  }
};
</script>