<template>
  <div class="task-creation-container">
    <div class="task-sub-creation-container">
      <input class="task-input" v-model="newTask" @keyup.enter="addTask" placeholder="What needs to be done?">
      <select @keyup.enter="addTask" class="status-input" v-model="status">
        <option value="New">New</option>
        <option value="In Progress">In Progress</option>
        <option value="Completed">Completed</option>
      </select>
      <button @click="addTask">Add</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      status: 'New', // Default status is "New"
      tasks: [], // Define and initialize the 'tasks' array
    };
  },
  methods: {
     addTask() {
    if (this.newTask.trim() !== '') {
      const task = {
        id: Date.now(),
        title: this.newTask,
        status: this.status,
        completed: false,
      };
      console.log(task.title)
      this.tasks.push(task);
      this.saveTasksToLocalStorage();
      this.$emit('add-task', task); // Emit the task object
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
.task-creation-container {
  display: flex;
  flex-direction: column;
  min-width: 100%;
  align-self: center;
  justify-content: center;
}
.task-sub-creation-container {
  display: flex;
  flex-direction: column;
  min-width: 100%;
  align-items: center;
  align-self: center;
  justify-content: center;
}
@media screen and (max-width: 768px) {
  .task-creation-container {
    padding-top: 5%;
  }
}
.status-input {
  padding-left: 10px;
  margin-right: 10px;
  height: 35px;
  width: 150px;
  border-radius: 5px;
  border: 1px solid gray;
  font-size: 18px;
  align-self: center;
  margin-top: 20px;
  outline: none;
  font-family: 'Times New Roman', Times, serif;
}
.task-input {
  padding-left: 10px;
  font-family: 'Times New Roman', Times, serif;
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
  .status-input {
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
  margin-top: 20px;
}
@media screen and (max-width: 768px) {
  button {
    width: 50px;
    font-size: 13px;
  }
}
</style>
