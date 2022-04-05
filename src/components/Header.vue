<template>
  <MyHeader>
    <h1> task tracker</h1>
  </MyHeader>
</template>

<script>
export default {
  name: 'MyHeader'
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
