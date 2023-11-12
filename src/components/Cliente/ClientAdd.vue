<!-- ClienteAdd.vue -->
<template>
  <div>
    <q-dialog v-model="mostrarModal" persistent>
    <q-card style="min-width: 450px">
      <q-card-section>
        <q-input v-model="edicion.nombre" autofocus label="Nombre persona/empresa*" />
      </q-card-section>
      <q-card-section>
        <q-input v-model="edicion.apellido" autofocus label="Apellido" />
      </q-card-section>
      <q-card-section>
        <q-input v-model="edicion.correoElectronico" autofocus label="Correo*" />
      </q-card-section>
      <q-card-section>
        <q-input v-model="edicion.telefono" autofocus label="Telefono*" />
      </q-card-section>
      <q-card-section>
        <q-input v-model="edicion.direccion" autofocus label="Direccion" />
      </q-card-section>
      <q-card-section>
        <q-select
          v-model="tipoDocumento"
          :options="tiposDocumento"></q-select>
          <q-input v-model="edicion.doc" autofocus label="Ingrese DNI/RUC*" />
      </q-card-section>
      <q-card-section>
        <q-input v-model="password" autofocus label="Contraseña" />
      </q-card-section>

        <!-- BOTONES -->
      <q-card-actions align="center" class="text-primary">
        <q-btn @click="guardarEdicion" label="Registrar" color="primary" v-close-popup/>


          <q-btn @click="cerrarModal" label="Cancelar" v-close-popup/>
      </q-card-actions>
    </q-card>
  </q-dialog>
  </div>
</template>

<style>
.titulo{
  text-align: center;
  font-size: large;
  font-style: inherit;
}
.qcard-modal-edit {
  width: 550px;
  align-content: center;
}

.buttons {
  display: flex;
  justify-content: space-between;
  margin-top: 25px;
}

.buttons q-btn {
  width: 48%;

}

.buttons q-btn:last-child {
  margin-left: 10px;
}

.custom-label .q-field__label {
font-size: 16px;

}
</style>



<script>
import axios from 'axios'
export default{
  data() {
    return {

      mostrarModal: false,
      edicion: {
        nombre: '',
        apellido: '',
        correo: '',
        telefono: '',
        direccion: '',
        dni: '',
        ruc: '',
        password: '',
      // Agrega más propiedades según sea necesario
      },
      tiposDocumento: ['DNI', 'RUC'],
      tipoDocumento: "DNI",
    };
  },


  mounted() {
      this.getClientes()

  },
  methods: {

      abrirModalnuevoC() {
          this.mostrarModal = true;
      },

          // Método para cerrar el modal de edición
      cerrarModal() {
          this.mostrarModal = false;
          // Limpia los campos de edición
          this.nuevoC = {
            nombre: '',
            apellido: '',
            correo: '',
            telefono: '',
            direccion: '',
            password: '',
            doc:'',
              // Limpia más propiedades según sea necesario
              };
      },

      // Método para enviar al servidor
      async guardarEdicion() {
      try {
          let url = "http://localhost:5243/api/Cliente/RegisterClient"
          var data = {}
          if (this.tipoDocumento === 'DNI') {
              data = {
                  nombre: this.edicion.nombre,
                  apellido: this.edicion.apellido,
                  correoElectronico: this.edicion.correoElectronico,
                  telefono: this.edicion.telefono,
                  direccion: this.edicion.direccion,
                  dni: this.edicion.doc,
                  password: this.edicion.password,
              };

          } else if (this.tipoDocumento === 'RUC') {
              data = {
                  nombre: this.edicion.nombre,
                  apellido: this.edicion.apellido,
                  correoElectronico: this.edicion.correoElectronico,
                  telefono: this.edicion.telefono,
                  direccion: this.edicion.direccion,
                  ruc: this.edicion.doc,
                  password: this.edicion.password,
              };
          }
          //console.log(data)
          //peticion post
          axios.post(url,data)
                  .then(reponse => {
                      this.$q.notify({
                          message: "Se añadió correctamente",
                          color: 'green',
                          position: 'top',
                          timeout: 10000
                      })
                      this.$emit('clienteAgregado');
                  }).catch(error => {
                      this.$q.notify({
                          message: "Ha Ocurrido un problema",
                          color: 'red',
                          position: 'top',
                          timeout: 10000
                      })
                  })



          getClientes();
          this.cerrarModal();
      } catch (error) {
          console.error('Error al actualizar:', error);
      }
      },

      async getClientes(){
          try {
          const response = await axios.get('http://localhost:5243/api/Cliente/GetAll');
          this.clientes = response.data;
          //console.log(this.clientes)
      } catch (error) {
          console.error('Error al obtener clientes:', error);
      }
      }


},
}
</script>
