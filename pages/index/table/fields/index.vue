<template>
  <div>
    <article>
      <h2>Table with checkbox</h2>
      <p>Working with fields</p>
      <br />
      <TableWithCheckbox> </TableWithCheckbox>
    </article>
    <br />
    <br />
    <!-- Table with dynamic textbox, select options and button -->
    <article>
      <h2>Table with dynamic textbox, select options and button</h2>
      <p>Dynamically add and remove fields</p>
      <br />

      <div>
        <form>
          <label>Customer </label>
          <input
            style="margin: 8px 0 8px"
            v-model="form.name"
            placeholder="Customer name"
          /><br />
          <label>Products</label>
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
                <td><input v-model.number="item.qty" /></td>
                <td><input v-model.number="item.unit_price" /></td>
                <!-- computeAmount -first parameter is quantity and
          we pass the item as second parameter to compute
          the unit price  -->
                <td>{{ item.qty | computeAmount(item) }}</td>
                <!-- remove item - i use filter to remove the item you can use other approach -->
                <td><button type="button" @click="remove(item)">x</button></td>
              </tr>
            </tbody>
          </table>

          <button type="button" style="margin-top: 10px" @click="add">
            Add New Entry
          </button>
          <br />
          <br />
          <!-- save button -->
          <button type="button" @click.prevent="onSave">Submit</button>
        </form>
        <hr style="margin-top: 30px" />
        <button @click="show_json_obj = !show_json_obj">
          {{ show_json_obj ? 'Hide ' : 'Show ' }}Json Object
        </button>

        <div v-show="show_json_obj" style="margin-top: 10px">
          <pre>form: {{ form }}</pre>
          <br />
          <pre>rows: {{ collections }}</pre>
        </div>
      </div>
    </article>
    <!-- Table with dynamic textbox, select options and button -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      show_json_obj: false,
      form: {},
      collections: [
        {
          id: 1,
          product: null,
          qty: null,
          unit_price: null,
          amount: 0,
        },
      ],
      categories: [
        { text: 'Category 1', value: 'Cat 1' }, //categories from database
        { text: 'Category 2', value: 'Cat 2' }, //categories from database
        { text: 'Category 3', value: 'Cat 3' }, //categories from database
      ],
      index: 0, //temporary id
    }
  },
  methods: {
    onSave() {
      this.form = {
        name: this.form.name,
        items: this.collections,
      }
      alert('Successfully submitted')
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
