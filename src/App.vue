<script>
export default {
  data() {
    return {
      city: "",
    };
  },
};
</script>

<template>
  <div class="wrapper">
    <h1>Weather app</h1>
    <p>Get known weather in {{ city }}</p>
    <input
      type="text"
      v-on:input="this.city = $event.target.value"
      placeholder="Write the name"
    />
    <button>Go!</button>
  </div>
</template>

<style scoped>
.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background-color: whitesmoke;
  text-align: center;
}

.wrapper h1 {
  margin-top: 50px;
}

.wrapper p {
  margin-top: 20px;
}

.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #ff9a3b;
  color: #ff9a3b;
  padding: 5px 8px;
  outline: none;
}

.wrapper input:focus {
  border-bottom: 2px solid #e77104;
}

.wrapper button {
  background: #ff9a3b;
  color: whitesmoke;
  border-radius: 10px;
  padding: 10px;
  border: none;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wrapper button:hover {
  transform: scale(1.1);
}
</style>
