<template>
  <div class="container">
    <MyHeader @toggle-add-task="toggleAddTask" :showAddTask="showAddTask" title="Диспетчер задач"/>
    <div v-show="showAddTask">
      <AddTask @add-task="addTask"/>
    </div>

    <MyTasks @toggle-reminder="$emit('toggleReminder')" @delete-task="deleteTask" :tasks="tasks"/>
  </div>
</template>

<script>
import MyHeader from "@/components/MyHeader";
import MyTasks from "@/components/MyTasks";
import AddTask from "@/components/AddTask";

export default {
  name: 'App',
  components: {
    AddTask,
    MyHeader,
    MyTasks
  },
  data () {
    return {
      tasks: [],
      showAddTask: true,
    }
  },
  methods: {
    toggleAddTask () {
      this.showAddTask = !this.showAddTask
    },
    async addTask (task) {
      const res = await fetch('http://localhost:3000/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task)
      }
      )
      const data = await res.json
      this.tasks = [...this.tasks, data]
    },
    async deleteTask (id) {
      if (confirm('Уверены?')){
        const res = await fetch(`http://localhost:3000/task${id}`, {
          method: 'DELETE'
        })
        res.status === 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id))
            : alert('Error deleting')
      }
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id)
      const updTask = {...taskToToggle, reminder: !taskToToggle.reminder}
      const res = await fetch(`http://localhost:3000/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updTask)
      })
      const data = await res.json()

      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: data.reminder } : task)
    },
    async fetchTask() {
      const res = await fetch(`http://localhost:3000/tasks`)

      const data = await res.json()

      return data
      }
    },
  async fetchTask(id) {
    const res = await fetch(`http://localhost:3000/tasks/${id}`)

    const data = await res.json()

    return data
  },
  async created () {
    this.tasks = await this.fetchTask()
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
  max-width: 500px;
  min-height: 300px;
  padding: 30px;
  overflow: auto;
  border-radius: 5px;
  margin: 30px auto;
}
.btn {
  display: inline-block;
  background: #2c3e50;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  font-size: 15px;
}
</style>
