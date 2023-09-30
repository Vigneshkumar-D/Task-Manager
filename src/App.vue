<template>
  <div class="task-manager-container">
    <h1 class="task-manager-title">Task Manager</h1>
    <div class="task-manager-sub-container">
      <TaskCreation @add-task="addTask"></TaskCreation>
      <div class="sub-container">
        <TaskFiltering :tasks="tasks" @filter-tasks="filterTasks"></TaskFiltering>
        <TaskDeletion @delete-completed-tasks="deleteCompletedTasks"></TaskDeletion>
      </div>
      <TaskList :tasks="filteredTasksArray" @initial-list="created" @update-task-status="handleUpdateTaskStatus" @delete-task="deleteTask" @mark-task-completed="markTaskCompleted"></TaskList>
    </div>
  </div>
</template>


<script>
import TaskCreation from './components/TaskCreation.vue';
import TaskList from './components/TaskList.vue';
import TaskDeletion from './components/TaskDeletion.vue';
import TaskFiltering from './components/TaskFiltering.vue';

export default {
  components: {
    TaskCreation,
    TaskList,
    TaskDeletion,
    TaskFiltering,
  },
  data() {
    return {
      tasks: [],
      selectedStatus: 'all',
      filteredTasksArray: [], 
    };
  },
  computed: {
    filteredTasks() {
      if (this.selectedStatus === 'all') {
        return this.tasks; // Show all tasks
      } else {
        return this.tasks.filter(task => task.taskStatus === this.selectedStatus);
      }
    },
  },
  methods: {
    addTask(newTask, status) {
      const task = {
        id: Date.now(),
        title: newTask,
        taskStatus: status,
        completed: false,
      };
      this.tasks.push(task);
      this.saveTasksToLocalStorage();
    },

    filterTasks(selectedStatus) {
      if (selectedStatus === 'all') {
        this.filteredTasksArray = this.tasks; // Show all tasks
      } else {
        this.filteredTasksArray = this.tasks.filter(task => task.taskStatus === selectedStatus);
      }
    },

    deleteTask(id) {
      // console.log(id)
      this.tasks = this.tasks.filter(task => task.id !== id);
      this.filteredTasksArray = this.tasks
      // console.log(this.tasks)
      this.saveTasksToLocalStorage();
    },

    deleteCompletedTasks() {
      this.tasks = this.tasks.filter(task => task.taskStatus !== "Completed");
      this.filteredTasksArray = this.tasks
      this.saveTasksToLocalStorage();
    },
  
    markTaskCompleted(taskId) {
      const task = this.tasks.find(task => task.id === taskId);
      if (task) {
        task.completed = true;
        this.saveTasksToLocalStorage();
      }
    },
    handleUpdateTaskStatus(updatedTask) {
    const taskIndex = this.tasks.findIndex(task => task.id === updatedTask.id);
    if (taskIndex !== -1) {
      this.tasks[taskIndex].taskStatus = updatedTask.taskStatus;
      this.saveTasksToLocalStorage();
    }
  },
    saveTasksToLocalStorage() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
  },

  created() {
    const storedTasks = localStorage.getItem('tasks');
    if (storedTasks) {
      this.tasks = JSON.parse(storedTasks);
    }
    this.filteredTasksArray = this.tasks
  },
};
</script>



<style scoped>
/* TaskCreation-specific styles */
.task-manager-container {
  display: flex;
  flex-direction: column;
  /* justify-content: center; */
  /* align-items: center; */
  min-height: 100vh;
  width: 100%;
}
.task-manager-sub-container {
  display: flex;
  flex-direction: column;
  width: 100%;
  align-self: center;
}
.task-manager-title {
  font-size: 35px;
  width: 100%;
  text-align: center;
  font-family: 'Times New Roman', Times, serif;
  box-shadow: 0px 8px 40px rgba(7, 7, 7, 0.08);
  margin-bottom: 5%;
  margin-top: 0px;
  padding: 5px;
}
@media screen and (max-width: 768px) {
  .task-manager-title {
    font-size: 25px;
  }
}

.sub-container {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  align-items: center;
  padding-top: 5%;
}
@media screen and (max-width: 768px) {
  .sub-container {
    padding-top: 8%;
  }
}
</style>
