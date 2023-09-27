<!-- <template>
  <div class="task-list-container">
    <div class="status-filter">
      <label>Show by Status:</label>
      <select class="options" v-model="selectedStatus" @change="updateFilter">
        <option value="all">All</option>
        <option value="New">New</option>
        <option value="In Progress">In Progress</option>
        <option value="Completed">Completed</option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    tasks: Array,
  },
  data() {
    return {
      selectedStatus: 'all',
    };
  },
  methods: {
    updateFilter() {
      this.$emit('filter-tasks', this.selectedStatus);
    },
  },
};
</script>

 <style scoped>
input {
  padding: 5px;
  margin-right: 10px;
  font-family: 'Times New Roman', Times, serif;
}
.options {
  height: 35px;
  font-family: 'Times New Roman', Times, serif;
  margin-left: 5px;
  font-size: 17px;
}

@media screen and (max-width: 768px) {
  .options {
    height: 25px;
    font-size: 13px;
  }
}
</style> -->