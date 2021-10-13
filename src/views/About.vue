<template>
  <div>
    <ul>
      <div v-for="(item, index) in items" :key="index">
        <div v-if="index % 2 === 0">
          <li>
            {{ item.mensaje }}
          </li>
        </div>
        <div v-if="index % 2 !== 0">
          <li style="color: red">
            {{ item.mensaje }}
          </li>
        </div>
      </div>
    </ul>
  </div>
</template>

<script>
export default {
  data: () => ({
    items: [
      { mensaje: "foo" },
      { mensaje: "Bar" },
      { mensaje: "Jarra" },
      { mensaje: "Teclado" },
      { mensaje: "Botella" },
      { mensaje: "Silla" },
    ],
  }),
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
