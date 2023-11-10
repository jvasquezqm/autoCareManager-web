<template>
  <div class="q-pa-md">
    <q-table
      grid="$q.screen.xs"
      flat bordered
      title="Clientes"
      :rows="filteredRows"
      :columns="columns"
      row-key="clienteId"
    >
    <template v-slot:top-right>
      <q-input  borderless dense debounce="300" v-model="filter" placeholder="Search" class="q-mb-md">
          <template v-slot:append>
                <q-icon name="search" />
          </template>
        </q-input>
    </template>
      <template v-slot:body="props">
        <q-tr :props="props">
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
      filter,
      filteredRows,
    };
  },
};
</script>

<style scoped>
/* Estilos personalizados según sea necesario */
</style>
