<template>
  <q-page>
    <q-page-container>
      <TableTemplate :columns="columns" :rows="rows" />
    </q-page-container>
  </q-page>
</template>

<script>
import axios from 'axios';
import TableTemplate from 'components/TableTemplate.vue';

export default {
  name : 'ClientGestion',
  components: {
    TableTemplate,
  },
  data() {
    return {
      columns: [
        { name: 'clienteId', label: 'ID Cliente' },
        { name: 'nombre', label: 'Nombre' },
        { name: 'apellido', label: 'Apellido' },
        { name: 'correoElectronico', label: 'Correo Electrónico' },
        { name: 'telefono', label: 'Teléfono' },
        { name: 'direccion', label: 'Dirección' },
        { name: 'dni', label: 'DNI' },
        { name: 'ruc', label: 'RUC' },
      ],
      rows: [],
    };
  },
  created() {
    // Llamada a la API cuando se crea la página
    this.fetchDataFromAPI();
  },
  methods: {
    fetchDataFromAPI() {
      // Reemplaza la siguiente URL con la URL de tu API
      var apiUrl = 'http://localhost:5243/api/Cliente/GetAll';

      axios.get(apiUrl)
        .then(response => {
          // Asigna los datos obtenidos de la API a la propiedad 'rows'
          this.rows = response.data;
        })
        .catch(error => {
          console.error('Error al obtener datos de la API:', error);
        });
    },
  },
};
</script>

<style scoped>
/* Estilos personalizados según sea necesario */
</style>
