<template>
  <div class="MyHeader">
    {{ title }}
    <MyButton text="Добавить задачу" color="teal"/>
  </div>
</template>

<script>
import MyButton from "@/components/MyButton";
export default {
  name: 'MyHeader',
  components: { MyButton },
  props: {
    title: {
      type: String,
      default: 'Hello world'
    }
  }
}
</script>

<style scoped>
.MyHeader {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  color: darkcyan;
  font-size: 25px;
}
</style>
