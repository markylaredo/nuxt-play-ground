<template>
  <div>
    <h3>Component v-model</h3>
    <CustomTextField v-model="value" />

    <br />
    <br />
    <p>Parent Value:{{ value }}</p>
  </div>
</template>
<script>
export default {
  data() {
    return {
      value: null,
    }
  },
}
</script>
>
