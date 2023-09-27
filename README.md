# Vue.js Task Manager

A simple task management application built with Vue.js that allows you to create, delete, filter, and mark tasks as completed.

## Features

- **Task Creation**: Add new tasks to the list.
- **Task Deletion**: Remove tasks from the list.
- **Task Filtering**: Filter tasks based on completion status (e.g., show only completed tasks or incomplete tasks).
- **Data Validation**: Ensure task titles are not empty.
- **Persistence**: Task data is persisted in the browser's local storage, so your tasks are saved even after refreshing the page.

## Project Structure

The project is organized as follows:

- `src/` directory contains the Vue.js application files.
  - `components/` directory houses the individual Vue components.
  - `App.vue` is the root component that assembles the application.
  - Other components include TaskCreation, TaskList, TaskDeletion, and TaskFiltering.
  - The application logic is handled in the Vue instance in `App.vue`.
- `public/` directory contains static assets such as CSS styles and icons.
- The project uses Vue.js for the front-end and local storage for data persistence.

## Getting Started

1. Clone the repository:

   ```bash
   git clone https://github.com/Vigneshkumar-D/Task-Manager.git
   ```

2. Navigate to the project directory:

   ```bash
   cd vue-task-manager
   ```

3. Install the project dependencies:

   ```bash
   npm install
   ```

4. Start the development server:

   ```bash
   npm run serve
   ```

5. Open your browser and visit [http://localhost:8080](http://localhost:8080) to access the Task Manager application.

## Usage

- **Adding a Task**: Enter a task description in the input field and press "Add Task."
- **Deleting a Task**: Click the delete button next to a task to remove it from the list.
- **Filtering Tasks**: Use the filtering options to show completed or incomplete tasks.
- **Marking a Task as Completed**: Click the checkbox next to a task to mark it as completed. The task text will turn red and have a strike-through.

## Data Persistence

Task data is stored in the browser's local storage, ensuring that your tasks are saved even after you close the browser or refresh the page.

## Contributing

Feel free to contribute to this project by opening issues or pull requests. Your feedback and contributions are highly appreciated.

## License

This project is licensed under the [MIT License](LICENSE).

---

Happy task management with Vue.js!
```

Please make sure to replace placeholders like `your-username` and update any additional information specific to your project. You can also include installation and deployment instructions or any other details that are relevant to your application.
