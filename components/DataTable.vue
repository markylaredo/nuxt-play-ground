<template>
  <div>
    <table>
      <thead>
        <tr>
          <th v-for="column in columns" :key="column.label">
            {{ column.label }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="row in currentRows" :key="row.id">
          <td v-for="column in columns" :key="column.key">
            {{ row[column.key] }}
          </td>
        </tr>
      </tbody>
    </table>
    <pagination
      :currentPage="currentPage"
      :perPage="perPage"
      :total="totalRows"
      @page-changed="pageChanged"
    />
  </div>
</template>

<script>
export default {
  name: 'DataTable',

  props: {
    perPage: {
      type: Number,
      default: 10,
    },
    columns: {
      type: Array,
      required: true,
    },
    items: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      currentPage: 1,
    }
  },
  computed: {
    totalRows() {
      return this.items.length
    },
    currentRows() {
      const start = (this.currentPage - 1) * this.perPage
      return this.items.slice(start, start + this.perPage)
    },
  },
  methods: {
    pageChanged(page) {
      this.currentPage = page
    },
  },
}
</script>
