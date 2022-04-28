<!--<template>-->
<!--  <div class="container">-->
<!--    <MyHeader @toggle-add-task="toggleAddTask" :showAddTask="showAddTask" title="Диспетчер задач"/>-->
<!--    <div v-show="showAddTask">-->
<!--      <AddTask @add-task="addTask"/>-->
<!--    </div>-->

<!--    <MyTasks @toggle-reminder="$emit('toggleReminder')" @delete-task="deleteTask" :tasks="tasks"/>-->
<!--  </div>-->
<!--</template>-->

<!--<script>-->
<!--import MyHeader from "@/components/MyHeader";-->
<!--import MyTasks from "@/components/MyTasks";-->
<!--import AddTask from "@/components/AddTask";-->

<!--export default {-->
<!--  name: 'App',-->
<!--  components: {-->
<!--    AddTask,-->
<!--    MyHeader,-->
<!--    MyTasks-->
<!--  },-->
<!--  data () {-->
<!--    return {-->
<!--      tasks: [],-->
<!--      showAddTask: true,-->
<!--    }-->
<!--  },-->
<!--  methods: {-->
<!--    toggleAddTask () {-->
<!--      this.showAddTask = !this.showAddTask-->
<!--    },-->
<!--    async addTask (task) {-->
<!--      const res = await fetch('http://localhost:3000/tasks', {-->
<!--        method: 'POST',-->
<!--        headers: {-->
<!--          'Content-type': 'application/json',-->
<!--        },-->
<!--        body: JSON.stringify(task)-->
<!--      }-->
<!--      )-->
<!--      const data = await res.json-->
<!--      this.tasks = [...this.tasks, data]-->
<!--    },-->
<!--    async deleteTask (id) {-->
<!--      if (confirm('Уверены?')){-->
<!--        const res = await fetch(`http://localhost:3000/task${id}`, {-->
<!--          method: 'DELETE'-->
<!--        })-->
<!--        res.status === 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id))-->
<!--            : alert('Error deleting')-->
<!--      }-->
<!--    },-->
<!--    async toggleReminder(id) {-->
<!--      const taskToToggle = await this.fetchTask(id)-->
<!--      const updTask = {...taskToToggle, reminder: !taskToToggle.reminder}-->
<!--      const res = await fetch(`http://localhost:3000/tasks/${id}`, {-->
<!--        method: 'PUT',-->
<!--        headers: {-->
<!--          'Content-type': 'application/json'-->
<!--        },-->
<!--        body: JSON.stringify(updTask)-->
<!--      })-->
<!--      const data = await res.json()-->

<!--      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: data.reminder } : task)-->
<!--    },-->
<!--    async fetchTask() {-->
<!--      const res = await fetch(`http://localhost:3000/tasks`)-->

<!--      const data = await res.json()-->

<!--      return data-->
<!--      }-->
<!--    },-->
<!--  async fetchTask(id) {-->
<!--    const res = await fetch(`http://localhost:3000/tasks/${id}`)-->

<!--    const data = await res.json()-->

<!--    return data-->
<!--  },-->
<!--  async created () {-->
<!--    this.tasks = await this.fetchTask()-->
<!--  }-->
<!--}-->
<!--</script>-->

<!--<style>-->
<!--.container {-->
<!--  font-family: Avenir, Helvetica, Arial, sans-serif;-->
<!--  -webkit-font-smoothing: antialiased;-->
<!--  -moz-osx-font-smoothing: grayscale;-->
<!--  text-align: center;-->
<!--  color: #2c3e50;-->
<!--  border: dashed;-->
<!--  max-width: 500px;-->
<!--  min-height: 300px;-->
<!--  padding: 30px;-->
<!--  overflow: auto;-->
<!--  border-radius: 5px;-->
<!--  margin: 30px auto;-->
<!--}-->
<!--.btn {-->
<!--  display: inline-block;-->
<!--  background: #2c3e50;-->
<!--  border: none;-->
<!--  padding: 10px 20px;-->
<!--  margin: 5px;-->
<!--  border-radius: 5px;-->
<!--  font-size: 15px;-->
<!--}-->
<!--</style>-->
<!--<template>
  <div class="container">
    <div id="app">
      <h1>Покупки</h1>
      <input v-model="itemName" @keyup.enter="addItem" type="text" /><br />
      <button @click="addItem()">Add Item</button>
    </div>
    <ul>
      <li
          v-for="item of items"
          :class="{ bought: item.bought }"
          :key="item.id"
          @click="boughtItem(item.id)"
          @dblclick="removeItem(item.id)"
      >
        {{ item.name }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      items: [],
      itemName: "",
    };
  },
  async created() {
    try {
      const res = await axios.get(`http://localhost:3000/items`);
      this.items = res.data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    async boughtItem(id) {
      await axios.patch(`http://localhost:3000/items/${id}`, {
        bought: true,
      });
      this.items = this.items.map((item) => {
        if (item.id === id) {
          item.bought = true;
        }
        return item;
      });
    },
    //on double clicking the item, it will call removeItem(id) method
    removeItem(id) {
      axios.delete(`http://localhost:3000/items/${id}`);
      this.items = this.items.filter((item) => item.id !== id);
    },
    //method for adding items in the list
    async addItem() {
      const res = await axios.post(`http://localhost:3000/items`, {
        name: this.itemName,
      });
      this.items = [...this.items, res.data];
      this.itemName = "";
    },
  },
};
</script>

<style>
#app {
  text-align: center;
  color: #2c3e50;
}
.container {
  background-color: #24e02dd2;
  max-width: 400px;
  margin: 0 auto;
  border-radius: 8px;
}
li {
  font-size: 1.5rem;
  list-style: none;
}
button {
  margin-top: 5px;
  background-color: #3498db;
  border: none;
  color: #ffffff;
  padding: 10px 20px;
  font-size: 14px;
  cursor: pointer;
  border-radius: 4px;
}
input {
  margin-top: 5px;
  padding: 10px 20px;
  font-size: 14px;
  border-radius: 4px;
}
.bought {
  text-decoration: line-through;
}
</style>-->
