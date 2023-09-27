<template>
  <div>
    <button @click="deleteCompletedTasks">Delete Completed Tasks</button>
  </div>
</template>

<script>
export default {
  methods: {
    deleteCompletedTasks() {
      this.$emit('delete-completed-tasks');
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


button {
  background-color: #FF2400;
  font-family: 'Times New Roman', Times, serif;
  height: 35px;
  border-radius: 5px;
  color: #fff;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  font-size: 20px;
}
@media screen and (max-width: 768px) {
  button {
  height: 25px;
  /* width: 50px; */
  font-size: 13px;
}
}
</style>
