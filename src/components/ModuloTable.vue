<template>
  <div class="table-wrapper">
    <table>
      <tr v-for="(rowValue) in row" :key="rowValue">
        <td
          v-bind:class="highlight(rowValue, columnValue)"
          v-for="(columnValue) in row"
          :key="columnValue"
        >{{getValue(rowValue, columnValue)}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "ModuloTable",
  methods: {
    getValue(x, y) {
      // return (x * y) % this.modulo;
      return x ** y % this.modulo;
    },
    highlight(x, y) {
      return {
        active: this.getValue(x, y) === 1,
        zero: this.getValue(x, y) === 0
      };
    },
    getArray(length) {
      const arr = [];
      for (let i = 1; i <= length; i++) {
        arr.push(i);
      }
      return arr;
    }
  },
  data: function() {
    return {
      modulo: 13,
      row: this.getArray(20)
    };
  }
};
</script>

<style scoped>
.active {
  background-color: yellow;
}
.zero {
  background-color: red;
}
.table-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 3em;
}
td {
  padding: 1em;
  width: 1em;
  height: 1em;
  border: 1px solid silver;
}
</style>