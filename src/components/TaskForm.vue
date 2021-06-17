<template>
  <form class="form" @submit.prevent="onSubmit()">
    <label class="form__label" for="task">Task</label>
    <input class="form__input" type="text" placeholder="Add task" id="task" v-model="task" />
    <label class="form__label" for="date">Day & Time</label>
    <input class="form__input" type="text" placeholder="Add date & time" id="date" v-model="date" />
    <label for="reminder">Set Reminder: </label>
    <input type="checkbox" v-model="reminder" id="reminder"/>
    <button class="form__btn">Save Task</button>
  </form>
</template>
<script>
export default {
  data () {
    return {
      task: '',
      date: '',
      reminder: false
    }
  },
  methods: {
    async onSubmit () {
      if (!this.task) {
        alert('Add task Name!')
        return
      }
      if (!this.date) {
        alert('Add date task!')
        return
      }
      const data = JSON.stringify({
        task: this.task,
        date: this.date,
        reminder: this.reminder
      })
      console.log(data)
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: data
      })
      const temp = await res.json()
      console.log(temp)
      this.$emit('task-add', temp)
      this.task = ''
      this.date = ''
      this.reminder = false
    }
  }
}
</script>

<style scoped lang="scss">

 label {
      color: #000;
 }
 .form {
 &__label {
     display: block;
     color: #000;
     margin-bottom: 5px;
 }
 &__input {
     display: block;
     max-width: 70%;
     margin: 0 auto;
     margin-bottom: 10px;
     padding: 7px 10px;
 }
 &__btn {
     display: block;
     margin: 15px auto;
     padding: 10px 15px;
     color:#FFF;
     background: #000;
     border-radius: 8px;
   border:none;
   font-family: 'Poppins' , sans-serif;
   font-weight: bold;
 }
 }
</style>
