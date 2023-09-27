<template>
  <div class="task-list-container">
    <!-- Dropdown to filter tasks by status -->
    <div class="status-filter">
      <label>Show by Status:</label>
      <select v-model="selectedStatus">
        <option value="all">All</option>
        <option v-for="status in uniqueStatuses" :key="status" :value="status">{{ status }}</option>
      </select>
    </div>

    <ul>
      <li class="task-list-item" v-for="task in filteredTasks" :key="task.id">
        <div>
          <input
            class="check-box"
            type="checkbox"
            v-model="task.completed"
            @change="markTaskCompleted(task)"
          />
          <span :class="{ 'completed-task': task.completed }">{{ task.title }}</span>

          <!-- Display and update the task's status with a dropdown -->
        </div>
        <div>
          <select class="status-options" v-model="task.status" @change="updateTaskStatus(task)">
            <option value="New">New</option>
            <option value="In Progress">In Progress</option>
            <option value="Completed">Completed</option>
          </select>
          <button @click="deleteTask(task.id)">Delete</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    tasks: Array,
  },
  data() {
    return {
      selectedStatus: 'all', // Default selected status is "All"
    };
  },
  computed: {
    // Extract unique status values from tasks
    uniqueStatuses() {
      const statuses = new Set();
      this.tasks.forEach(task => {
        statuses.add(task.status);
      });
      return Array.from(statuses);
    },
    filteredTasks() {
      if (this.selectedStatus === 'all') {
        return this.tasks; // Return all tasks if "All" is selected
      } else {
        // Filter tasks based on selected status
        return this.tasks.filter(task => task.status === this.selectedStatus);
      }
    },
  },
  methods: {
    deleteTask(id) {
      this.$emit('delete-task', id);
    },
    markTaskCompleted(task) {
      // Emit an event to notify the parent component that a task is marked as completed
      this.$emit('mark-task-completed', task.id);
    },
    updateTaskStatus(task) {
      // Find the index of the task in this.tasks and update its status
      const index = this.tasks.findIndex(t => t.id === task.id);
      if (index !== -1) {
        this.tasks[index].status = task.status;
        // Emit an event to notify the parent component that a task's status has been updated
        this.$emit('update-task-status', this.tasks[index]);
      }
    },
  },
};
</script>

<style scoped>
/* TaskList-specific styles */
.task-list-container {
  display: flex;
  flex-direction: column;
  align-self: center;
  width: 50%;
  padding-top: 3%;
}
@media screen and (max-width: 768px) {
  .task-list-container {
    width: 90%;
  }
}
ul {
  list-style-type: none;
  padding: 6px;
}
.check-box {
  margin-right: 15px;
}
.task-list-item {
  margin: 5px 0;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0px 8px 40px rgba(7, 7, 7, 0.08);
  font-size: 20px;
  padding: 6px;
  border-radius: 5px;
  font-family: 'Times New Roman', Times, serif;
}
@media screen and (max-width: 768px) {
  .task-list-item {
    font-size: 13px;
    width: 100%;
  }
}
button {
  background-color: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  border-radius: 5px;
  height: 35px;
  align-self: flex-end;
  font-size: 20px;
}
@media screen and (max-width: 768px) {
  button {
    height: 25px;
    font-size: 13px;
  }
}
.completed-task {
  color: red;
  text-decoration: line-through;
}
select {
  padding: 5px;
  border-radius: 5px;
}
.status-filter {
  margin-bottom: 10px;
}
.status-options {
  margin-right: 15px;
  align-self: center;
}
</style>
