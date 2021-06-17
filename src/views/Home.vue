<template>
  <div class="home">
    <Header @add-task="addTask"></Header>
    <TaskHolder @delete-task="deleteTask" v-bind:tasks="tasks" />
  </div>
</template>

<script>
import Header from '@/components/Header.vue'
import TaskHolder from '@/components/TaskHolder.vue'
export default {
  name: 'Home',
  data () {
    return { tasks: [] }
  },
  components: {
    Header,
    TaskHolder
  },
  async created () {
    const res = await fetch('http://localhost:3000/tasks')
    const data = await res.json()
    console.log(data)
    this.tasks = data
  },
  methods: {
    async deleteTask (id) {
      await fetch(`api/tasks/${id}`, {
        method: 'DELETE',
        headers: {
          'Content-Type': 'application/json'
        }
      })
      this.tasks = this.tasks.filter((x) => {
        if (x.id !== id) {
          return x
        }
      })
    },
    addTask (task) {
      this.tasks.push(task)
    }
  }
}
</script>
<style lang="scss" scoped>
.home {
  margin: 0 auto;
  max-width: 350px;
  border: 3px solid #9da5af;
  border-radius: 5px;
  padding: 10px 15px;
}
</style>
