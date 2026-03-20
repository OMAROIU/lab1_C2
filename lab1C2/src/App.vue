<template>
  <div class="container">
    <h1>Lista de Tareas</h1>

    <!-- INPUT -->
    <input v-model="nuevaTarea" placeholder="Escribe una tarea">

    <!-- BOTON -->
    <button @click="agregarTarea">Agregar</button>

    <!-- VALIDACION -->
    <p v-if="error" style="color:red">{{ error }}</p>

    <!-- LISTA -->
    <ul>
      <li v-for="(tarea, index) in tareas" :key="index">
        {{ tarea }}
        <button @click="eliminar(index)">X</button>
      </li>
    </ul>

    <!-- CONTADOR -->
    <p>Total tareas: {{ tareas.length }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nuevaTarea: "",
      tareas: [],
      error: "",
      usuario: "Omar",
      activo: true
    }
  },
  methods: {
    agregarTarea() {
      if (this.nuevaTarea === "") {
        this.error = "No puede estar vacío"
        return
      }

      this.tareas.push(this.nuevaTarea)
      this.nuevaTarea = ""
      this.error = ""
    },
    eliminar(index) {
      this.tareas.splice(index, 1)
    }
  }
}
</script>