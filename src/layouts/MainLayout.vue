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
            @click="cambiarRuta(tab.name)"
          />
          <q-menu v-if="activeTab === 'cliente'">
            <q-list link>
              <q-item @click="cambiarRuta('cliente')">cliente</q-item>
              <q-item @click="cambiarRuta('vehiculo')">Vehículos</q-item>
            </q-list>
          </q-menu>
        </q-tabs>
        <!-- Botón de Cerrar Sesión -->
        <q-btn
          flat
          dense
          round
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
import { useRoute } from 'vue-router';
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
      this.$router.push('/');

    },
    cambiarRuta(name) {
      this.$router.push(`/dashboard/${name}`);

      if (name === 'client' || name === 'vehiculo') {

      } else {
        switch (name) {
          case 'home':
            this.$router.push('/dashboard');
            break;
          case 'gestionTaller':
            this.$router.push('/gestion-taller');
            break;
          case 'propietario':
            this.$router.push('/dashboard/propietario');
            break;
          case 'cliente':
            this.$router.push('/dashboard/client'); // Cambia la ruta a "/cliente"
            break;
          case 'vehiculo':
            this.$router.push('/dashboard/vehiculo'); // Cambia la ruta a "/vehiculo"
            break;
          case 'servicios':
            this.$router.push('/dashboard/servicios');
            break;
          case 'facturas':
            this.$router.push('/dashboard/facturas');
            break;
          case 'inventario':
            this.$router.push('/dashboard/inventario');
            break;
          case 'reportes':
            this.$router.push('/dashboard/reportes');
            break;
          default:
            break;
        }
      }
    },
  },

  setup () {
    var route = useRoute();
    var leftDrawerOpen = ref(false)

    return {
      activeTab: 'home', // Nombre de la pestaña activa inicial
      tabs: [
        { name: 'home', label: 'Home' },
        { name: 'gestionTaller', label: 'Gestión Taller' },
        { name: 'propietario', label: 'Gestión Propietarios' },
        { name: 'cliente', label: 'Gestion cliente' },
        { name: 'vehiculo', label: 'Vehiculo' },

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
