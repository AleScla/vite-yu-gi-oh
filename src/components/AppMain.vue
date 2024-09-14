<script>
import {store} from '../store.js';
export default {
  data(){
    return{
      store
    }
  },
  props:{
    cardsFound: Number,
    cards: Array,
  },
  methods:{
    changeCards(){
      this.$emit('changeCards')
    },
    resetValue(){
      this.$emit('resetValue')
    }
  }
}
</script>


<template>
 <main class="bg-warning">
  <div class="container">
    <!-- 3) Utilizzo del componente -->
    <section class="card-section text-start ">
      <button @click="resetValue">RESET</button>
      <select @change="changeCards()" v-model="store.selectValue" class="my-2">
        
        <option v-for="(archetype, index) in store.allArchetypes" :key="index" :value="archetype.archetype_name">{{ archetype.archetype_name }}</option>
      </select>
      <div class="container cards-container p-5">
        <div class="row">
          <div class="col-12 p-0">
            <div class="container"><!-- NUMERO DI CARTE TROVATO -->
              <div class="row">
                <div class="col-12 cards-found text-start bg-secondary py-3">
                  Found {{ cardsFound }} cards
                </div>
              </div>
            </div>
            <div class="container">
              <div class="row">
                <div class="col-3 p-0" v-for="card, i in cards" :key="i">
                  <div class="card px-1">
                    <img :src="card.card_images[0].image_url" class="card-img-top" alt="carta">
                    <div class="card-body px-0 text-center">
                      <h5 class="card-text cardname">{{card.name}}</h5>
                      <p class="card-text archetype">{{card.archetype}}</p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
 </main>
</template>

<style lang="scss" scoped>
@use '../assets/scss/partials/variables' as *;
 
  main{
  min-height:100vh;
  .cards-container{
  background-color:white;
    .cards-found{
      color:white;
      font-weight:bold;
    }
    .card{
    border:none;
    }
  }

}


</style>
