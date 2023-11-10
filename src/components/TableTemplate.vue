<template>
  <div class="q-pa-md">
    <q-table
      grid="$q.screen.xs"
      flat bordered
      title="Treats"
      :rows="filteredRows"
      :columns="columns"
      :filter="filter"
      row-key="clienteId"
    >
      <template v-slot:top-right>
        <q-input  borderless dense debounce="300" v-model="filter" placeholder="Search" class="q-mb-md">
          <template v-slot:append>
                <q-icon name="search" />
              </template>
        </q-input>
      </template>

      <!-- area donde se redenriza el body -->
      <template v-slot:body="props">
        <!-- fila de la tabla -->
        <q-tr :props="props">
          <!-- celda de la tabla -->
          <q-td
            v-for="col in props.cols"
            :key="col.name"
            :props="col.props"
          >
            {{ props.row[col.name] }}
          </q-td>
        </q-tr>
      </template>
    </q-table>
  </div>
</template>

<script>
import { ref, computed, watch } from 'vue';

export default {
  props: {
    columns: {
      type: Array,
      required: true,
    },
    rows: {
      type: Array,
      required: true,
    },
  },
  setup(props) {
    const filter = ref('');

    const filteredRows = computed(() => {
      const lowerCaseFilter = filter.value.toLowerCase();
      return filter.value
        ? props.rows.filter(row => {
            return props.columns.some(col => {
              const cellValue = String(row[col.name]).toLowerCase();
              return cellValue.includes(lowerCaseFilter);
            });
          })
        : props.rows;
    });

    watch(() => props.rows, () => {
      // Cuando cambian las filas, reseteamos el filtro
      filter.value = '';
    });

    return {
      filter: ref(''),
      filteredRows,
    };
  },
};
</script>

<style scoped>
/* Estilos personalizados según sea necesario */
</style>
