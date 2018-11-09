<template>
  <div id="Header">
    <img src="../../static/animal-dose-logo.png" alt="logo">
    <p>Your daily dose of random animal facts!</p>
  </div>
</template>
<script>
export default {
  name: "Header",
}
</script>
<style scoped>
  #Header {
    display: flex;
    flex-flow: row;
    justify-content: space-between;
    width: 100vw;
    height: 12vh;
  }
  img {
    height: 7vh;
    padding: 0 2vw;
    align-self: center;
  }
  p {
    font-family: 'Montserrat', sans-serif;
    padding-bottom: 2vh;
  }
</style>
