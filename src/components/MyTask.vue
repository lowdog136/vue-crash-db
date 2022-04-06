<template>
  <div :class="[task.reminder ? 'reminder' : '', 'task']">
    <div class="title_task">
      {{ task.text }}
      <p style="font-style: oblique">{{ task.day }}</p>
    </div>
    <h2><i @click="onDelete()" class="fas fa-times"></i></h2>
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
.title_task{
  font-size: 16px;
  margin: 0 15px;
}
.task.reminder {
  border-left: 5px solid #0c850c;
}
.fas {
  color: red;
  margin: 15px;
}
.task {
  display: flex;
  align-items: center;
  margin: 5px;
  justify-content: space-between;
  background: #efd89e;
}
</style>
