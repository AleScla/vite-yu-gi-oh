<script>
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import axios from 'axios';
import {store} from './store.js'

export default {
  
  data() {
    return { 
      store
    }
  },
  created() {
    this.filterAPI()
    this.archetypeAPI()
  },
  // 2) Dichiarazione del componente
  components: {
    AppHeader,
    AppMain,
  },
  methods:{
    filterAPI(){
      axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0',
          {
            params:{
              archetype: this.store.selectValue
            }
          })
          .then((res)=>{
            console.log(res.data)
            this.store.allCards = res.data.data;
            console.log(this.store.selectValue)
            
          })
          .catch((err) =>{
            this.store.selectValue = [];
          })
    },
    archetypeAPI(){
      axios.get('https://db.ygoprodeck.com/api/v7/archetypes.php')
        .then((res) =>{
          console.log(res.data)
          for (let i = 0; i < 100; i++){
            let singleData = res.data[i];
            this.store.allArchetypes.push(singleData)
          }
          console.log('archetipi', this.store.allArchetypes)
      })
    },
    resetPage(){
      this.store.selectValue = [];
      this.filterAPI()
    }

  }}
</script>

<template>
 <AppHeader />
 <AppMain :cardsFound="store.allCards.length" :cards="store.allCards" @resetValue="resetPage()" @changeCards="filterAPI()"/>
</template>

<style lang="scss">
@use 'assets/scss/main' as *;


// Import all of Bootstrap's CSS
@import "bootstrap/scss/bootstrap";
</style>
