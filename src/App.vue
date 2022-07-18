<template>
  <div id="app">
    <button v-on:click="add">add new row</button>
    <p>Total price {{ total }} | {{ total2 }}</p>

    <ul>
      <li v-for="(item, index) in items">
        Name<br />
        <input type="text" v-model="item.name" />
        <br />

        Quantity<br />
        <input type="number" v-model.number="item.quantity" min="1" />
        <br />

        Price<br />
        <input
          type="number"
          v-model.number="item.price"
          min="0.00"
          max="1000000000.00"
          step="0.01"
        />
        <br />

        Total (readonly) <br />
        <input v-model="totalItem(item)" readonly /> <br />

        total in row:
        {{ totalItem(item) }}
        <br />
        <br />

        <button v-on:click="remove(index)">Delete row</button>
        <hr />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      items: [
        { name: 'A', quantity: 1, price: 20 },
        { name: 'B', quantity: 2, price: 30 },
      ],
    };
  },
  methods: {
    add() {
      this.items.push({
        name: '',
        quantity: '',
        price: '',
      });
    },
    remove(index) {
      this.items.splice(index, 1);
    },
    totalItem(item) {
      return item.price * item.quantity;
    },
  },
  computed: {
    total() {
      let sum = 0;
      this.items.forEach((item) => {
        sum += parseFloat(item.price) * parseFloat(item.quantity);
      });

      return sum;
    },
    // another approach how to sum
    total2() {
      return this.items.reduce((prev, item) => {
        return prev + item.price * item.quantity;
      }, 0);
    },
  },
};
</script>
