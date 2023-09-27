<!-- <template>
    <div>
      
      <label>Show by Status:
        <select v-model="selectedStatus">
          <option value="all">All</option>
          <option value="New">New</option>
          <option value="In Progress">In Progress</option>
          <option value="Completed">Completed</option>
        </select>
      </label>
  
      
      <ul>
        <li v-for="task in filteredTasks" :key="task.id">
          {{ task.title }} - {{ task.status }}
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        tasks: [
          { id: 1, title: 'Task 1', status: 'New' },
          { id: 2, title: 'Task 2', status: 'In Progress' },
          { id: 3, title: 'Task 3', status: 'Completed' },
          // Add more tasks here
        ],
        selectedStatus: 'all', // Default selected status is "All"
      };
    },
    computed: {
      filteredTasks() {
        if (this.selectedStatus === 'all') {
          return this.tasks; // Return all tasks if "All" is selected
        } else {
          // Filter tasks based on selected status
          return this.tasks.filter(task => task.status === this.selectedStatus);
        }
      },
    },
  };
  </script>
   -->

   <template>
    <div>
      <!-- Add a dropdown to filter tasks by status -->
      <label>Show by Status:
        <select @change="filterTasks">
          <option value="all">All</option>
          <option value="New">New</option>
          <option value="In Progress">In Progress</option>
          <option value="Completed">Completed</option>
        </select>
      </label>
  
      <!-- Task list -->
      <ul>
        <li v-for="task in filteredTasks" :key="task.id">
          {{ task.title }} - {{ task.status }}
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        tasks: [
          { id: 1, title: 'Task 1', status: 'New' },
          { id: 2, title: 'Task 2', status: 'In Progress' },
          { id: 3, title: 'Task 3', status: 'Completed' },
          // Add more tasks here
        ],
        selectedStatus: 'all', // Default selected status is "All"
      };
    },
    computed: {
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
      filterTasks() {
        // You can add additional logic here if needed
        // For now, just recompute the filtered tasks based on the selected status
        this.filteredTasks = this.tasks.filter(task => {
          return this.selectedStatus === 'all' || task.status === this.selectedStatus;
        });
      },
    },
  };
  </script>
  