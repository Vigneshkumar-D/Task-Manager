<template>
  <div class="task-manager-container">
    <h1 class="task-manager-title">Task Manager</h1>
    <div class="task-manager-sub-container">
      <TaskCreation @add-task="addTask"></TaskCreation>
      <div class="sub-container">
        <TaskFiltering :tasks="tasks" @filter-tasks="filterTasks"></TaskFiltering>
        <TaskDeletion @delete-completed-tasks="deleteCompletedTasks"></TaskDeletion>
      </div>
      <TaskList :tasks="filteredTasks" @delete-task="deleteTask" @mark-task-completed="markTaskCompleted"></TaskList>
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
    };
  },
  computed: {
    filteredTasks() {
      if (this.filter === 'completed') {
        return this.tasks.filter(task => task.completed);
      } else if (this.filter === 'incomplete') {
        return this.tasks.filter(task => !task.completed);
      } else {
        return this.tasks;
      }
    },
  },
  methods: {
    addTask(newTask) {
      const task = {
        id: Date.now(),
        title: newTask,
        completed: false,
      };

      this.tasks.push(task);
      this.saveTasksToLocalStorage();
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id);
      this.saveTasksToLocalStorage();
    },
    deleteCompletedTasks() {
      this.tasks = this.tasks.filter(task => !task.completed);
      this.saveTasksToLocalStorage();
    },
    filterTasks(filter) {
      this.filter = filter;
    },
    markTaskCompleted(taskId) {
      const task = this.tasks.find(task => task.id === taskId);
      if (task) {
        task.completed = true;
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
