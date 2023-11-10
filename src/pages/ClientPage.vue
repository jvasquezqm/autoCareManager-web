<template>
  <div class="product-page">
    <div class="q-ml-md q-mr-xl">
      <ClientGestion />
    </div>
  </div>
</template>
<style>
.product-page {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}




</style>
<script>
import ClientGestion from "src/components/Gestion/ClientGestion.vue";
export default {
  name: "ClientPage",
  components: {
    ClientGestion,

  }
};

</script>
