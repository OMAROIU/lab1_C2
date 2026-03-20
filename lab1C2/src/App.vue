<template>
  <div class="container">
    <h1>Gestor de Tareas</h1>

    <!-- INPUT -->
    <input v-model="nuevaTarea" placeholder="Escribe una tarea">

    <!-- BOTÓN -->
    <button @click="agregarTarea">Agregar tarea</button>

    <!-- ERROR -->
    <p v-if="error" style="color:red">{{ error }}</p>

    <!-- FILTROS -->
    <div style="margin-top:15px; display:flex; gap:5px;">
      <button @click="filtro='todas'">Todas</button>
      <button @click="filtro='pendientes'">Pendientes</button>
      <button @click="filtro='completadas'">Completadas</button>
    </div>

    <!-- LISTA -->
    <ul>
      <li v-for="(tarea, index) in tareasFiltradas" :key="index">
        
        <!-- TEXTO -->
        <span 
          :style="{ textDecoration: tarea.completada ? 'line-through' : 'none' }"
          @click="toggleTarea(index)"
        >
          {{ tarea.texto }}
        </span>

        <!-- BOTÓN ELIMINAR -->
        <button @click="eliminar(index)">X</button>
      </li>
    </ul>

    <!-- CONTADOR -->
    <p>Total: {{ tareas.length }}</p>
    <p>Completadas: {{ tareasCompletadas }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nuevaTarea: "",
      tareas: [],
      error: "",
      filtro: "todas",
      usuario: "Omar" // variable extra (para cumplir requisito)
    }
  },
  computed: {
    tareasFiltradas() {
      if (this.filtro === "pendientes") {
        return this.tareas.filter(t => !t.completada)
      }
      if (this.filtro === "completadas") {
        return this.tareas.filter(t => t.completada)
      }
      return this.tareas
    },
    tareasCompletadas() {
      return this.tareas.filter(t => t.completada).length
    }
  },
  methods: {
    agregarTarea() {
      if (this.nuevaTarea.trim() === "") {
        this.error = "No puedes dejar el campo vacío"
        return
      }

      this.tareas.push({
        texto: this.nuevaTarea,
        completada: false
      })

      this.nuevaTarea = ""
      this.error = ""
    },

    eliminar(index) {
      this.tareas.splice(index, 1)
    },

    toggleTarea(index) {
      this.tareas[index].completada = !this.tareas[index].completada
    }
  }
}
</script>