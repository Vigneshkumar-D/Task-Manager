<template>
    <div class="task-creation-container">
      <input class="task-input" v-model="newTask" @keyup.enter="addTask" placeholder="What needs to be done?">
      <button @click="addTask">Add</button>
    </div>
  </template>
  
  <script>
  export default {
  data() {
    return {
      newTask: '',
      tasks: [], // Define and initialize the 'tasks' array
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        const task = {
          id: Date.now(),
          title: this.newTask,
          completed: false,
        };

        this.tasks.push(task); // Push the task to the 'tasks' array
        this.saveTasksToLocalStorage(); // Save tasks to local storage

        this.$emit('add-task', this.newTask);
        this.newTask = '';
      }
    },
    saveTasksToLocalStorage() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
  },
};

</script>
<style scoped>
/* TaskCreation-specific styles */
.task-creation-container{
    display: flex;
    flex-direction: row;
    min-width: 100%;
    align-self: center;
    justify-content: center;
}
@media screen and (max-width: 768px) {
  .task-creation-container{
    padding-top: 5%;
}
}
.task-input {
  padding-left: 10px;
  margin-right: 10px;
  height: 35px;
  width: 30%;
  border-radius: 5px;
  border: 1px solid gray;
  font-size: 20px;
}
@media screen and (max-width: 768px) {
  .task-input {
  height: 25px;
  width: 50%;
  font-size: 13px;
}
}

button {
  background-color: #4caf50;
  color: #fff;
  border: none;
  font-family: 'Times New Roman', Times, serif;
  padding: 5px 10px;
  cursor: pointer;
  width: 100px;
  border-radius: 5px;
  font-size: 20px;
}
@media screen and (max-width: 768px) {
  button {
  width: 50px;
  font-size: 13px;
}
}
</style>
