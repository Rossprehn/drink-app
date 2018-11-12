<template>
  <div id="Footer">
    <p>© 2018, Ross Prehn</p>

  </div>
</template>
<script>
export default {
  name: "Footer",
}
</script>
<style scoped>
#Footer {
  display: flex;
  flex-flow: row;
  justify-content: space-between;
  width: 100vw;
}
p {
  align-self: flex-end;
  padding: 0 2vw;
}
</style>
