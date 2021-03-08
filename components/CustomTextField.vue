<template>
  <div >
    <input
      class="c-input"
      :value="value"
      v-on:input="$emit('input', $event.target.value)"
    />
    
  </div>
</template>
<style scoped>
.c-input {
  padding: 5px;
  color: red;
  border: 2px solid green;
}
</style>
<script>
export default {
  props: {
    value: null,
  },
  data() {
    return {}
  },
  methods: {},
}
</script>
