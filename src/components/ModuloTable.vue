<template>
  <div>
    <div>
      Current modulo: {{ modulo }}.
      <button v-if="modulo > 1" @click="changeModulo(-1)">-1</button>
      <button @click="changeModulo(1)">+1</button>
    </div>
    <div class="table-wrapper">
      <table>
        <th></th>
        <!-- Keys workaround from https://github.com/vuejs/vue/issues/7323 -->
        <th v-for="rowValue in row" :key="'col' + rowValue">{{ rowValue }}</th>
        <tr v-for="(rowValue) in row" :key="'row' + rowValue" v-bind:class="highlightRow(rowValue)">
          <th>{{ rowValue }}</th>
          <td
            v-bind:class="highlight(rowValue, columnValue)"
            v-for="(columnValue) in row"
            :key="columnValue"
          >{{getValue(rowValue, columnValue)}}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "ModuloTable",
  methods: {
    getValue(x, y) {
      // return (x * y) % this.modulo;
      // return x ** y % this.modulo;

      // Calculate x ** y manually, with a loop.
      // This way we can take the result modulo this.modulo after each multiplication
      // which avoids using big numbers and getting wrong answers.
      // We could do the same with the faster algorithm from the previous exercise.
      let res = 1;
      for (let i=0; i<y; i++) res = (res * x) % this.modulo;
      return res;
    },
    highlight(x, y) {
      return {
        active: this.getValue(x, y) === 1,
        zero: this.getValue(x, y) === 0
      };
    },
    highlightRow(x) {
      // Checks if x and this.modulo are coprime (they have no common divisors).
      // It can be done much faster using Euclidean algorithm.
      for (let i=2; i<=Math.min(x, this.modulo); i++)
        if (x%i === 0 && this.modulo%i === 0)
          return { notcoprime: true };
      return { coprime: true };
    },
    getArray(length) {
      const arr = [];
      for (let i = 1; i <= length; i++) {
        arr.push(i);
      }
      return arr;
    },
    changeModulo(diff) {
      this.modulo += diff;
    }
  },
  data: function() {
    return {
      modulo: 25,
      row: this.getArray(30)
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
.coprime {
  opacity: 0.8;
}
.notcoprime {
  opacity: 0.4  ;
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
