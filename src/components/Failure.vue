<template>
  <div class="container">
    <h1>Malesef Bilemediniz!!!</h1>
    <button @click="newGame">Yeni Oyun</button>
  </div>
</template>

<script>
export default {
  methods: {
    newGame() {
      this.$emit("activeComponentEvent", "app-Game-Cards");
    },
  },
};
</script>

<style scoped>
.container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: darkred;
}

.container h1 {
  text-align: center;
  font-size: 333%;
  color: white;
}

.container button {
  cursor: pointer;
  width: 200px;
  background-color: #fff;
  color: darkred;
  border: 1px solid brown;
  height: 50px;
  font-size: 15px;
  border-radius: 5px;
  outline: none;
}

.container button:hover {
  background-color: lightgreen;
  color: #fff;
  transition: all 0.5s;
}
</style>
