<template>
  <div>
    <!-- ... Resto del código ... -->

    <!-- Modal para la edición -->
    <q-dialog v-model="mostrarModal">
      <q-card>
        <q-card-section>
          <q-input v-model="edicion.nombre" label="Nombre" />
          <q-input v-model="edicion.apellido" label="Apellido" />
          <!-- Agrega más campos de edición según sea necesario -->

          <q-btn @click="guardarEdicion" label="Guardar" color="primary" />
          <q-btn @click="cerrarModal" label="Cancelar" />
        </q-card-section>
      </q-card>
    </q-dialog>
  </div>
</template>

<script>
import { ref } from 'vue';
import { useQuasar } from 'quasar';
import axios from 'axios';

export default {
  data() {
    return {
      // ... Resto del código ...
      mostrarModal: false,
      edicion: {
        nombre: '',
        apellido: '',
        // Agrega más propiedades según sea necesario
      },
    };
  },

  methods: {
    // ... Resto del código ...

    // Método para abrir el modal de edición
    abrirModalEdicion(fila) {
      // Guarda la fila seleccionada para editar
      this.edicion = { ...fila };
      this.mostrarModal = true;
    },

    // Método para cerrar el modal de edición
    cerrarModal() {
      this.mostrarModal = false;
      // Limpia los campos de edición
      this.edicion = {
        nombre: '',
        apellido: '',
        // Limpia más propiedades según sea necesario
      };
    },

    // Método para guardar la edición y enviarla al servidor
    async guardarEdicion()
    {
      try {
        const response = await axios.put(`http://localhost:5243/api/Cliente/Update/${this.edicion.clienteId}`, this.edicion);
        console.log('Registro actualizado:', response.data);
        // Actualiza tus datos después de editar
        this.getDatos();
        // Cierra el modal
        this.cerrarModal();
      } catch (error) {
        console.error('Error al actualizar:', error);
      }
    },
  },
};
</script>
