<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated >
      <q-toolbar>
    <q-tabs
      v-model="activeTab"
      align="center"
      class="bg-primary text-white"
    >
      <q-tab
        v-for="(tab, index) in tabs"
        :key="index"
        :label="tab.label"
        :name="tab.name"
      />

    </q-tabs>
    <!-- Botón de Cerrar Sesión -->
    <q-btn flat dense round
      icon="exit_to_app"
      @click="cerrarSesion"
      class="q-ml-auto"

    />
  </q-toolbar>
    </q-header>


    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'



export default defineComponent({
  name: 'MainLayout',

  components: {
    // EssentialLink
  },
  methods: {
    cerrarSesion() {
      // Lógica para cerrar sesión
      console.log('Cerrar Sesión');
      // Puedes redirigir a la página de inicio de sesión, por ejemplo:
      // this.$router.push('/login');
    },
  },

  setup () {
    var leftDrawerOpen = ref(false)

    return {
      activeTab: 'perfil', // Nombre de la pestaña activa inicial
      tabs: [
        { name: 'perfil', label: 'Perfil' },
        { name: 'gestionTaller', label: 'Gestión Taller' },
        { name: 'clientes', label: 'Gestion Clientes' },
        { name: 'servicios', label: 'Servicios' },
        { name: 'facturas', label: 'Facturas' },
        { name: 'inventario', label: 'Inventario' },
        { name: 'reportes', label: 'Reportes' },
      ],

      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }

    }
  }
})
</script>
