<template>
  <nav>
    <ul class="pagination">
      <li v-if="currentPage > 1" @click="pageChanged(currentPage - 1)">
        <a href="#" aria-label="Previous">
          <span aria-hidden="true">&laquo;</span>
        </a>
      </li>
      <li
        v-for="page in pages"
        :key="page"
        :class="{ active: page === currentPage }"
        @click="pageChanged(page)"
      >
        <a href="#">{{ page }}</a>
      </li>
      <li v-if="currentPage < totalPages" @click="pageChanged(currentPage + 1)">
        <a href="#" aria-label="Next">
          <span aria-hidden="true">&raquo;</span>
        </a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  props: {
    currentPage: {
      type: Number,
      required: true,
    },
    perPage: {
      type: Number,
      default: 10,
    },
    total: {
      type: Number,
      required: true,
    },
  },
  computed: {
    totalPages() {
      return Math.ceil(this.total / this.perPage)
    },
    pages() {
      const pages = []
      for (let i = 1; i <= this.totalPages; i++) {
        pages.push(i)
      }
      return pages
    },
  },
  methods: {
    pageChanged(page) {
      this.$emit('page-changed', page)
    },
  },
}
</script>

<style  scoped>
.pagination {
  display: flex;
  justify-content: center;
  list-style: none;
  padding: 0;
}

.pagination li {
  display: inline-block;
  margin: 0 5px;
}

.pagination li.active {
  font-weight: bold;
}

.pagination li a {
  text-decoration: none;
}

.pagination li a:hover,
.pagination li a:focus {
  color: #23527c;
}

</style>
