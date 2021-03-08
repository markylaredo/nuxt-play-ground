<template>
  <div class="container">
    <div class="container-column">
      <!-- table -->
      <table class="table-border">
        <thead>
          <tr>
            <th>
              <input type="checkbox" v-model="checkAll" id="all" /><label
                for="all"
                >&nbsp;All</label
              >
            </th>
            <th>Products/Services</th>
            <th>Qty</th>
            <th>Unit Price</th>
            <th>Status</th>
            <th>Amount</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in items" :key="item.id">
            <td>
              <input
                :disabled="item.isSubmitted"
                v-model="item.isCheck"
                type="checkbox"
              />
            </td>
            <td>{{ item.product }}</td>
            <td><input v-model="item.qty" placeholder="Qty" /></td>
            <td>{{ item.unit_price }}</td>
            <td>{{ item.isSubmitted }}</td>
            <td>{{ item | totalPrice }}</td>
          </tr>
        </tbody>
      </table>
      <!-- end table -->
    </div>
    <!-- submit button -->
    <button @click="submitHandler">Submit</button>
    <!-- Json object -->
    <hr style="margin-top: 30px" />

    <div class="container-item">
      <!-- button show hide -->
      <button @click="show_json_obj = !show_json_obj">
        {{ show_json_obj ? 'Hide ' : 'Show ' }}Json Object
      </button>
      <!-- end button show hide -->
      <div v-show="show_json_obj" style="margin-top: 10px">
        <pre style="width: 300px">selectedItems:{{ selectedItems }}</pre>
        <pre>checkAll:{{ checkAll }}</pre>
        <pre>items:{{ items }}</pre>
      </div>
    </div>
    <!-- end Json object -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      show_json_obj: false,
      checkAll: false,
      selectedItems: [],
      items: [
        {
          id: 1,
          isCheck: false,
          product: 'Product',
          qty: 23,
          unit_price: 39,
          isSubmitted: false,
        },
        {
          id: 2,
          isCheck: false,
          product: 'Product 2',
          qty: 65,
          unit_price: 30,
          isSubmitted: false,
        },
        {
          id: 3,
          isCheck: false,
          product: 'Product 3',
          qty: 3,
          unit_price: 28.27,
          isSubmitted: false,
        },
      ],
    }
  },
  methods: {
    submitHandler() {
      alert(JSON.stringify(this.selectedItems))
      this.markItemAsSubmitted()
    },
    async markItemAsSubmitted() {
      for (let i = 0; i < this.selectedItems.length; i++) {
        const el = this.selectedItems[i]

        let item = this.items.find((f) => f.id === el.id)
        if (item) {
          item.isSubmitted = true
        }
      }

      //clear all item selected
      //add delay to clear the selectedItems and
      //This will add a little delay to clear the selectedItems
      await this.$nextTick(() => {
        this.selectedItems = []
      })
    },
  },
  watch: {
    checkAll(_data) {
      this.items.forEach((el) => {
        if (!el.isSubmitted) {
          el.isCheck = _data
        }
        //TODO: your other code here
      })
    },
    items: {
      deep: true,
      handler(_data) {
        this.selectedItems = _data
          .map((item) => {
            //check if the item is not submitted then...
            if (item.isCheck && !item.isSubmitted) {
              //this will remove the isCheck property
              const { isCheck, ...res } = item
              return res
            }
          })
          .filter((e) => e)
      },
    },
  },
  filters: {
    totalPrice(item) {
      return item.qty * item.unit_price
    },
  },
}
</script>

<style scoped>
.container-row {
  display: flex;
  flex-flow: row wrap;
  padding: 0;
  margin: 0;
  margin: 10px;
  padding: 20px;
}
.container-column {
  display: flex;
  flex-flow: column wrap;
  padding: 0;
  margin: 0;
  margin: 10px;
  padding: 20px;
}
button {
  width: fit-content;
}

.container-item {
  /* padding: 5px;*/
  width: 300px;
}
</style>
