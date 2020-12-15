<template>
  <div style="margin: 100px">
    <h3>Working with dynamic fields</h3>
    <form>
      <input
        style="margin: 8px 0 8px"
        v-model="form.name"
        placeholder="Customer name"
      />
      <table class="table-border">
        <thead>
          <tr>
            <th>Products/Services</th>
            <th>Qty</th>
            <th>Unit Price</th>
            <th>Amount</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in collections" :key="item.id">
            <td>
              <!-- selection start -->
              <select v-model="item.product">
                <option
                  v-for="opt in categories"
                  :key="opt.value"
                  :value="opt.value"
                >
                  {{ opt.text }}
                </option>
              </select>
              <!-- selection end -->
            </td>
            <td><input v-model="item.qty" /></td>
            <td><input v-model="item.unit_price" /></td>
            <!-- computeAmount -first parameter is quantity and  
          we pass the item as second parameter to compute 
          the unit price  -->
            <td>{{ item.qty | computeAmount(item) }}</td>
            <!-- remove item - i use filter to remove the item you can use other approach -->
            <td><button type="button" @click="remove(item)">x</button></td>
          </tr>
        </tbody>
      </table>

      <button type="button" @click="add">Add New Entry</button>
      <br />
      <br />
      <!-- save to database -->
      <button type="button" @click.prevent="onSave">Save to Db</button>
    </form>
    <!-- end save to database -->
    <hr style="margin-top: 30px" />
    <div style="margin-top: 10px">
      <pre>form: {{ form }}</pre>
      <br />
      <pre>collections: {{ collections }}</pre>
    </div>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: 'Nuxt play ground 🤪',
    }
  },
  data() {
    return {
      form: {},
      collections: [],
      categories: [
        { text: 'Category 1', value: 'Cat 1' }, //categories from database
        { text: 'Category 2', value: 'Cat 2' }, //categories from database
        { text: 'Category 3', value: 'Cat 3' }, //categories from database
      ],
      index: 0, //mimicking the id
    }
  },
  methods: {
    onSave() {
      this.form = {
        name: this.form.name,
        items: this.collections,
      }
    },
    add() {
      //ugly but it does its job
      this.index++ //temporary id you can use better approach than this 😂 for demo purposes

      //this will add new entry in collections
      this.collections.push({
        id: this.index, //grab the new id,
        product: null,
        qty: null, //quantity
        unit_price: null, //price per unit
        amount: null, //price per unit
      })
    },
    remove(item) {
      this.collections = this.collections.filter((el) => el.id !== item.id)
    },
  },
  filters: {
    computeAmount(qty, item) {
      let total = qty * item.unit_price
      item.amount = total
      return total
    },
  },
}
</script>

<style>
table,
th,
td {
  border: 1px solid black;
}
.container {
  margin: 0 auto;
  min-height: 100vh;
  /* display: flex; */
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
