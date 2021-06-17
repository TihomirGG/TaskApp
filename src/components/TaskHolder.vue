<template>
  <main>
      <div v-for="task in tasks" :key="task.id">
      <TaskCard @delete-task="$emit('delete-task', task.id)"  :task="task"/>
      </div>
  </main>
</template>

<script>
import TaskCard from './TaskCard.vue'
export default {
  props: {
    tasks: Array
  },
  components: { TaskCard },
  emits: ['delete-task']
}
</script>

<style>
</style>
