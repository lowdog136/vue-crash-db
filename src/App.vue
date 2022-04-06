<template>
  <div class="container">
    <MyHeader title="Диспетчер задач"/>
    <MyTasks @delete-task="deleteTask" :tasks="tasks"/>
  </div>
</template>

<script>
import MyHeader from "@/components/MyHeader";
import MyTasks from "@/components/MyTasks";

export default {
  name: 'App',
  components: {
    MyHeader, MyTasks
  },
  data () {
    return {
      tasks: []
    }
  },
  methods: {
    deleteTask (id) {
      this.tasks = this.tasks.filter((task) => task.id !== id)
    }

  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Поход на футбол',
        day: '19 апреля 17:00',
        reminder: true
      },
      {
        id: 2,
        text: 'Поездка на велосипеде',
        day: '12 апреля 11:00',
        reminder: true
      },
      {
        id: 3,
        text: 'Налоговая',
        day: '22 апреля 10:00',
        reminder: false
      }
    ]
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
