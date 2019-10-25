<template>
  <div class="pa-2">
    <v-row no-gutters>
      <v-col cols="12" sm="6" md="9" lg="10" class="pa-1">
        <v-card
          :loading="loading"
          width="100%"
          outlined
          :style="'height:' + cardHeight+ 'px;overflow-y:auto;overflow-x:hidden'"
        >
          <v-row class="pa-1" align="center">
            <v-col cols="12" class="headline font-weight-light text-center">Amount</v-col>
            <v-col cols="12" class="px-5 pt-5">
              <v-slider
                v-model="amountSlider"
                step="10"
                min="500"
                max="5000"
                :thumb-size="30"
                @end="end"
                thumb-label="always"
                hide-details
              ></v-slider>
            </v-col>
            <v-col cols="12" class="text-center">{{amountSlider}} USD</v-col>
          </v-row>
          <v-divider></v-divider>
          <v-row class="pa-1">
            <v-col cols="12" class="headline font-weight-light text-center">Number Of Payments</v-col>
            <v-col cols="12" class="px-5 pt-5">
              <v-slider
                v-model="monthsSlider"
                min="6"
                max="24"
                @end="end"
                :thumb-size="30"
                thumb-label="always"
                hide-details
              ></v-slider>
            </v-col>
            <v-col cols="12" class="text-center">{{monthsSlider}} months</v-col>
          </v-row>
          <v-divider></v-divider>
          <v-row class="pa-1">
            <v-col cols="12" class="headline font-weight-light text-center">Interest</v-col>
            <v-col cols="12" class="px-5 text-center">
              <LatestInterest :cacheItem="cache[cache.length - 1]" />
            </v-col>
          </v-row>
        </v-card>
      </v-col>
      <v-col cols="12" sm="6" md="3" lg="2" class="pa-1">
        <SideBar />
      </v-col>
    </v-row>
  </div>
</template>

<script>
// @ is an alias to /src
import SideBar from "../components/SideBar";
import axios from "axios";
import LatestInterest from "../components/LatestInterest";
export default {
  name: "home",
  components: {
    SideBar,
    LatestInterest
  },
  mounted() {
    this.cardHeight = window.innerHeight - 90;
    window.addEventListener("resize", () => {
      this.cardHeight = window.innerHeight - 90;
    });

    let localStorageCache = JSON.parse(localStorage.cache);
    this.cache = localStorageCache;
    this.amountSlider = this.cache[this.cache.length - 1].principal.amount;
    this.monthsSlider = this.cache[this.cache.length - 1].numPayments;
  },
  data: () => ({
    amountSlider: 500,
    monthsSlider: 6,
    loading: false,
    cache: [],
    cardHeight: 0
  }),
  watch: {
    cache(newValue) {
      localStorage.cache = JSON.stringify(newValue);
    }
  },
  methods: {
    end() {
      let amount = this.amountSlider;
      let numMonths = this.monthsSlider;
      let isCache = false;
      let index = -1;
      let cacheItem = {};
      this.cache.forEach((elem, i) => {
        if (elem.numPayments == numMonths && elem.principal.amount == amount) {
          isCache = true;
          index = i;
        }
      });
      if (isCache) {
        cacheItem = this.cache[index];
        this.cache.push(cacheItem);
      } else {
        this.calculate(amount, numMonths);
      }
    },
    calculate(amount, numMonths) {
      let self = this;
      this.loading = true;
      axios
        .get("https://ftl-frontend-test.herokuapp.com/interest", {
          params: {
            amount,
            numMonths
          }
        })
        .then(function(response) {
          if (response.status == "200") {
            self.cache.push(response.data);
            self.loading = false;
          }
        })
        .catch(function(error) {
          console.log(error);
        });
    }
  }
};
</script>
