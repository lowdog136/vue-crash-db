<template>
  <div :class="[task.reminder ? 'reminder' : '', 'task']">
    <h3>{{ task.text }}
      <p>{{ task.day }}</p>
    </h3>
    <i @click="onDelete()" class="fas fa-times"></i>
  </div>
</template>

<script>
export default {
  name: "MyTask",
  props: {
    task: Object
  },
  methods: {
    onDelete (id) {
      this.$emit('delete-task', id)
    }
  }
}
</script>

<style scoped>
.task.reminder {
  border-left: 5px solid green;
}
.fas {
  color: red;
}
.task {
  display: flex;
  align-items: center;
  margin: 5px;
  justify-content: space-between;
  background: #efd89e;
}
</style>
