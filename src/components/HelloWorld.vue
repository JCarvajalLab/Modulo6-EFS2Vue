<template>
  <div class="hello">
    <h1>Listado de Tareas</h1>
    <div class="input-container">
      <input v-model="newTask" type="text" placeholder="Agregar nueva tarea" />
      <button @click="addTask">Agregar Tarea</button>
    </div>

    <ul class="task-list">
      <li v-for="(task, index) in tasks" :key="index" class="task-item">
        <input v-model="task.text" class="task-input" :disabled="!task.isEditing" />
        <button @click="editTask(index)" class="edit-button">{{ task.isEditing ? 'Guardar' : 'Editar' }}</button>
        <button @click="deleteTask(index)" class="delete-button">Eliminar</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      newTask: '',
      tasks: [] // Inicializa la lista de tareas
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ text: this.newTask, isEditing: false }); // Agregar la propiedad isEditing
        this.newTask = ''; // Limpiar la caja de texto
      }
    },
    editTask(index) {
      const task = this.tasks[index];
      task.isEditing = !task.isEditing; // Cambiar el estado de edición
      if (!task.isEditing) {
        console.log('Guardando tarea:', task.text); // Puedes agregar lógica para guardar cambios si es necesario
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    }
  }
}
</script>

<style scoped>
.hello {
  max-width: 600px;
  margin: 0 auto;
  font-family: Arial, sans-serif;
}

h1 {
  text-align: center;
  color: #333;
}

.input-container {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

input[type="text"] {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-right: 10px;
  font-size: 16px;
}

button {
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.edit-button {
  background-color: #007bff;
  color: white;
}

.edit-button:hover {
  background-color: #0056b3;
}

.delete-button {
  background-color: #dc3545;
  color: white;
  margin-left: 5px;
}

.delete-button:hover {
  background-color: #c82333;
}

.task-list {
  list-style-type: none; /* Elimina los puntos de la lista */
  padding: 0; /* Elimina el padding */
}

.task-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  margin-bottom: 10px;
  background-color: #f9f9f9;
}

.task-input {
  flex: 1;
  border: none;
  outline: none;
  font-size: 16px;
  padding: 5px;
}
</style>