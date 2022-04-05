<template>
  <div class="MyHeader">
    <h1> {{ title }}</h1>
  </div>
</template>

<script>
export default {
  name: 'MyHeader',
  props: {
    title: {
      type: String,
      default: 'Hello world'
    }
  }
}
</script>

<style scoped>
MyHeader {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
