<template>
    <div>
      <label>Show:
        <select class="options" v-model="filter">
          <option value="all">All</option>
          <option value="completed">Completed</option>
          <option value="incomplete">Incomplete</option>
        </select>
      </label>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        filter: 'all',
      };
    },
    watch: {
      filter(newVal) {
        // Emit an event to notify the parent component to apply the filter
        this.$emit('filter-tasks', newVal);
      },
    },
  };
  </script>
  <style scoped>
  /* TaskCreation-specific styles */
  input {
    padding: 5px;
    margin-right: 10px;
  }
  .options{
    height: 35px;
  }
  
  @media screen and (max-width: 768px) {
  .options{
    height: 25px;
    font-size: 13px;
  }
}

  </style>
  