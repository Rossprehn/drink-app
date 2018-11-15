<template>
  <div id='app'>
    <Header />
     <div v-if="loading" id="loading-div">
      <img :src=leftCocktail alt="cockTail outline" class="cockTail-line" id="cockTail-left">
      <img :src=tigerOutline alt="tiger outline" id="tiger-outline">
      <div id="loading-button-div">
        <img @click="loading = !loading" @mouseover="hoverEnterBtnSrc" @mouseout="changeEnterBtnSrc" :src=buttonOutline alt="" id="enter-btn">
      </div>
      <img @click="loading = !loading" @mouseover="hoverEnterBtnSrc" @mouseout="changeEnterBtnSrc" :src=buttonOutline alt="" id="enter-btn-small">
      <img :src=rightcockTail alt="cockTail outline" class="cockTail-line" id="cockTail-right">
    </div>
    <main v-else>
      <img :src=leftCocktail alt='cockTail outline' class='cockTail-line' id='cockTail-left'>
      <div id='app-body'>
        <DrinkCard :recipe='currentRecipe'/>
      </div>
    </main>
    <Footer />
  </div>
</template>

<script>
import DrinkCard from './components/DrinkCard'
import Header from './components/Header'
import Footer from './components/Footer'

export default {
  name: 'App',
  components: {
    DrinkCard,
    ButtonContainer,
    Header,
    Footer
  },
  data() {
    return {
      apiURL: 'https://drinks-backend.herokuapp.com/',
      comments: [],
      drinkData: [],
      currentRecipe: {},
      currentComments: [],
      lastTenDrinks: []
    }
  },
  mounted() {
    this.getDrinks()
  },
  methods: {
    getDrinks() {
      fetch(this.apiURL)
        .then(res => res.json())
        .then(res => {
          this.recipeData = res.recipes
          this.chooseRandomRecipe()
          this.getComments()
          return res
        })
    },
    getComments() {
      fetch(this.apiURL + 'comments')
        .then(res => res.json())
        .then(json => {
          this.comments = json.comments
          this.getCommentsForCurrentDrink()
          return json
        })
    },
    chooseRandomRecipe() {
      let tempNum = Math.floor(Math.random() * this.recipeData.length)
      let drinkId = this.recipeData[tempNum].drink_id
      if(this.lastTenDrinks.includes(drinkId)){
        console.log('repeat', drinkId)
        this.chooseRandomRecipe()
      } else {
        this.setLengthOfLastTenDrinks()
        this.lastTenDrinks.push(drinkId)
        this.currentRecipe = this.recipeData[tempNum]
        return this.lastTenDrinks
      }
    },
    setLengthOfLastTenDrinks() {
      if(this.lastTenDrinks.length > 25){
        this.lastTenDrinks.shift()
        this.setLengthOfLastTenDrinks()
      }
    },
    getCommentsForCurrentDrink() {
      return this.currentComments = this.comments.filter(comment => comment.drink_id === this.currentRecipe.drink_id)
    }
  }
}
</script>

<style>

@import url('https://fonts.googleapis.com/css?family=Averia+Serif+Libre|Montserrat');

#app {
  text-align: center;
  display: flex;
  flex-flow: column;
  justify-content: flex-start;
  align-items: center;
  line-height: 1.6;
  width: 100vw;
  min-height: 100vh;
}

</style>
