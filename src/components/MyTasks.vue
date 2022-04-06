<template>
  <div class="task" v-for="task in tasks" :key="task.id">
    <MyTask @toggle-reminder="$emit('toggle-reminder', task.id)" @delete-task="$emit('delete-task', task.id)" :task="task" />
  </div>
</template>

<script>
import MyTask from "@/components/MyTask";
export default {
  name: "MyTasks",
  components: { MyTask },
  emits: ['delete-task', 'toggle-reminder'],
  props: {
    tasks: Array
  }
}
</script>

<style scoped>
.task {
  text-align: left;
  color: dimgray;
}
</style>
