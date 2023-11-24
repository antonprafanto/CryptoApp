<template>
  <ion-app>
    <ion-header>
      <ion-toolbar>
        <ion-title>Crypto App</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <ion-table>
        <ion-header>
          <ion-row>
            <ion-col>Name</ion-col>
            <ion-col>Symbol</ion-col>
            <ion-col>Price USD</ion-col>
          </ion-row>
        </ion-header>
        <ion-body>
          <ion-row v-for="crypto in cryptos" :key="crypto.id">
            <ion-col>{{ crypto.name }}</ion-col>
            <ion-col>{{ crypto.symbol }}</ion-col>
            <ion-col>{{ crypto.price_usd }}</ion-col>
          </ion-row>
        </ion-body>
      </ion-table>
      <ion-spinner v-if="loading" class="centered"></ion-spinner>
    </ion-content>
  </ion-app>
</template>



<script>
import { IonApp, IonContent, IonHeader, IonTitle, IonToolbar, IonList, IonItem, IonLabel, IonSpinner } from '@ionic/vue';
import { defineComponent } from 'vue';
import axios from 'axios';

export default defineComponent({
  name: 'App',
  components: {
    IonApp,
    IonContent,
    IonHeader,
    IonTitle,
    IonToolbar,
    IonList,
    IonItem,
    IonLabel,
    IonSpinner
  },
  data() {
    return {
      cryptos: [],
      loading: false
    }
  },
  methods: {
    fetchCryptos() {
      this.loading = true;
      axios.get('https://api.coinlore.net/api/tickers/')
        .then(response => {
          this.cryptos = response.data.data;
          this.loading = false;
        })
        .catch(error => {
          console.error(error);
          this.loading = false;
        })
    }
    
  },
  mounted() {
    this.fetchCryptos();
  }
});

</script>

<style>
.centered {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
</style>

