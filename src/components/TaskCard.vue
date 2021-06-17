<template>
  <div :class="['card', task.reminder ? 'card--green-border' : '']">
    <div class="card__info" @dblclick="onDblClick()">
      <h2 class="card__title">{{task.task}}</h2>
      <p class="card__date">{{task.date}}</p>
    </div>
    <i @click="deleteTask(task.id)" class="fas fa-times"></i>
  </div>
</template>

<script>
export default {
  props: {
    task: { type: Object, required: true }
  },
  methods: {
    async onDblClick () {
      this.task.reminder = !this.task.reminder
      const res = await fetch(`api/tasks/${this.task.id}`, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(this.task)
      })
      const temp = await res.json()
      console.log(temp)
    },
    deleteTask (id) {
      console.log(id)
      this.$emit('delete-task', id)
    }
  }
}
</script>

<style scoped lang="scss">
.fas {
  align-self: center;
  color: red;
  font-size: 20px;
}

.card {
  display: flex;
  background: #f2f2f2;
  justify-content: space-between;
  padding: 10px 10px;
  margin-bottom: 5px;
  &__title {
    font-size: 18px;
    margin: 0;
    color: #000;
    font-family: "Poppins", sans-serif;
  }

  &__date {
    font-size: 16px;
    margin: 0;
    margin-top: 5px;
    color: #000;
    font-family: "Poppins", sans-serif;
  }

}
  .card--green-border {
      border-left: 5px solid green;

  }
</style>
