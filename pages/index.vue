<template>
  <div>
    <button @click="cmpVModel">Component v-model</button>
    <button @click="dynamicFields">Table dynamic fields</button>
    <div class="container">
      <nuxt-child />
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    cmpVModel() {
      this.$router.push('/v-model-in-component')
    },
    dynamicFields() {
      this.$router.push('/table/fields')
    },
  },
}
</script>
