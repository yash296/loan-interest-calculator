<template>
  <div>
    <v-card outlined v-for="(historyItem,i) in history" :key="i" class="mb-3">
      <v-row>
        <v-col cols="12" md="6">
          <div class="text-center">
            Interest Rate
            <v-icon>mdi-arrow-right-bold-outline</v-icon>
            {{historyItem.interestRate}}
          </div>
        </v-col>
        <v-col cols="12" md="6">
          <div class="text-center">
            Monthly Payment
            <v-icon>mdi-arrow-right-bold-outline</v-icon>
            {{historyItem.monthlyPayment.amount}} {{historyItem.monthlyPayment.currency}}
          </div>
        </v-col>
        <v-col cols="12" md="6">
          <div class="text-center">
            Number Of Payments
            <v-icon>mdi-arrow-right-bold-outline</v-icon>
            {{historyItem.numPayments}}
          </div>
        </v-col>
        <v-col cols="12" md="6">
          <div class="text-center">
            Principal
            <v-icon>mdi-arrow-right-bold-outline</v-icon>
            {{historyItem.principal.amount}} {{historyItem.principal.currency}}
          </div>
        </v-col>
      </v-row>
    </v-card>
  </div>
</template>
<script>
export default {
  props: {
    history: {
      type: Array,
      default() {
        return [];
      }
    }
  }
};
</script>