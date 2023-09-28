<template>
  <div class="task-list-container">
    <ul>
      <li class="task-list-item" v-for="task in filteredTasks" :key="task.id">
        <div>
          <input
            class="check-box"
            type="checkbox"
            :checked="task.taskStatus === 'Completed'"
            v-model="task.completed"
            @change="markTaskCompleted(task)"
          />
          <span :class="{ 'completed-task': task.taskStatus=== 'Completed' }">{{ task.title }}</span>
        </div>
        <div>
          <select class="status-options" v-model="task.taskStatus" selected="task.taskStatus" @change="updateTaskStatus(task)">
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
    filteredTasksArray: Array
  },
  data() {
    return {
      selectedStatus: 'all', // Default selected status is "All"
    };
  },
  computed: {
    filteredTasks() {
      // console.log(this.tasks)
      if (this.selectedStatus === 'all') {
        return this.tasks ; // Return all tasks if "All" is selected
      } else {
        // Filter tasks based on selected status
        return this.tasks.filter(task => task.taskStatus === this.selectedStatus);
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

    updateFilter() {
      this.$emit('filter-tasks', this.selectedStatus);
    },
     
    updateTaskStatus(task) {
  // Emit an event to notify the parent component that a task's status has changed
      // console.log(task)
      this.$emit('update-task-status', task);
    }

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
  background-color: #FF2400;
  font-family: 'Times New Roman', Times, serif;
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
  color: #FF2400;
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
  font-size: 17px;
  align-self: center;
  font-family: 'Times New Roman', Times, serif;
}
@media screen and (max-width: 768px) {
  .status-options {
    font-size: 13px;
    width: 100px;
  }
}
</style>
