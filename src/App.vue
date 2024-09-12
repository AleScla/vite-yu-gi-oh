<script>
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import axios from 'axios'

export default {
  
  data() {
    return { 
      allCards:[]
    }
  },
  created() {
    axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0')
    .then((res)=>{
      console.log(res.data)
      this.allCards = res.data.data;
      console.log('a', res.data.data)
      console.log(this.allCards)
    })
  },
  // 2) Dichiarazione del componente
  components: {
    AppHeader,
    AppMain,
  },
}
</script>

<template>
 <AppHeader />
 <AppMain :cardsFound="allCards.length" :cards="allCards"/>

</template>

<style lang="scss">
@use 'assets/scss/main' as *;


// Import all of Bootstrap's CSS
@import "bootstrap/scss/bootstrap";
</style>
