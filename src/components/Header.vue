/*//
<template>
  <header>
    <div class="header">
      <h2 class="header__title">Task Tracker</h2>
      <button
        @click="onClick"
        :class="['header__btn', showForm ? 'red' : 'green']"
      >
        {{ showForm ? "Close" : "Add Task" }}
      </button>
    </div>
    <TaskForm @task-add="addTask" :class="[showForm ? '' : 'hidden']" />
  </header>
</template>

<script>
import TaskForm from './TaskForm.vue'
export default {
  data () {
    return { showForm: false }
  },
  components: { TaskForm },
  methods: {
    onClick () {
      this.showForm = !this.showForm
    },
    addTask (task) {
      this.$emit('add-task', task)
    }
  }
}
</script>

<style scoped lang="scss">
.header {
  display: flex;
  justify-content: space-between;
  font-family: "Poppins", sans-serif;
  &__title {
      color:#000;
  }
  &__btn {
    align-self: center;
    flex-basis: 25%;
    font-weight: bold;
    padding: 10px 10px;
    font-family: "Poppins", sans-serif;
    border-radius: 8px;
    border: none;
    color: #fff;
  }
  &_btn:hover {
    cursor: pointer;
  }
}
.red {
    background: red;
}
.green {
    background: #007600;
}
.hidden {
  display: none;
}
</style>
