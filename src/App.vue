<template>
  <div class="container">
    <MyHeader title="Task Tracker"/>
  </div>
</template>

<script>
import MyHeader from "@/components/MyHeader";

export default {
  name: 'App',
  components: {
    MyHeader
  }
}
</script>

<style>
.container {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  border: dashed;
  margin-top: 60px;
}
</style>
