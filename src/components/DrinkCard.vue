<template>
  <div id="DrinkCard">
    <h2>{{recipe.name}}</h2>
    <p id="ingerence">{{recipe.ingerence}}</p>
    <img :src="recipe.image" alt="please wait for server load" />
    <p id="recipe-description">{{recipe.recipe}}</p>
  </div>
</template>

<script>
export default {
  name: "DrinkCard",
  data: () => ({
  }),
  props: ["recipe"]
}</script>

<style scoped>
  #DrinkCard {
    display: flex;
    flex-flow: column;
    align-items: center;
    background-color: white;
    padding: 2vmin;
    border-radius: 5px;
  }
  #ingerence {
    font-style: italic;
  }
  img {
    max-width: 70vmin;
    max-height: 60vmin;
    border-radius: 5px;
  }
  h2 {
    font-weight: 400;
    font-size: 2rem;
    line-height: 1;
    font-family: 'Averia Serif Libre', cursive;
  }
  p {
    font-size: 1rem;
    width: 70vmin;
    text-align: center;
    font-family: 'Montserrat', sans-serif;
    font-weight: 100;
  }
</style>
