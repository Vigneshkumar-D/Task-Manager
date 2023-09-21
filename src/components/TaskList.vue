<template>
  <div class="task-list-container">
    <ul>
      <li class="task-list-item" v-for="task in tasks" :key="task.id">
        <div>
          <input
            class="check-box"
            type="checkbox"
            v-model="task.completed"
            @change="markTaskCompleted(task)"
          />
          <span :class="{ 'completed-task': task.completed }">{{ task.title }}</span>
      </div>
        <button @click="deleteTask(task.id)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    tasks: Array,
  },
  methods: {
    deleteTask(id) {
      this.$emit('delete-task', id);
    },
    markTaskCompleted(task) {
      // Emit an event to notify the parent component that a task is marked as completed
      this.$emit('mark-task-completed', task.id);
    },
  },
};
</script>

<style scoped>
  /* Import the CSS file for TaskList.vue */  
  /* TaskList-specific styles */
  .task-list-container{
    display: flex;
    flex-direction: column;
    align-self: center;
    width: 50%;
    padding-top: 3%;
  }
  @media screen and (max-width: 768px) {
    .task-list-container{
    width: 90%;
  }
}
  ul {
    list-style-type: none;
    padding: 6px;
  }
  .check-box{
    margin-right: 15px;
  }
  .task-list-item{
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
    .task-list-item{
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
  </style>
  