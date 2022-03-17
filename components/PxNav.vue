<template>
  <b-nav vertical class="px-2 pt-4 mr-1">
    <b-avatar class="ml-3" src="@/src/images/logo.jpg" size="10rem"></b-avatar>
    <b-nav-item active>Módulo de Catalogos</b-nav-item>
    <b-nav-item>Módulo de Solicitudes</b-nav-item>
    <b-nav-item>Reportería</b-nav-item>
  </b-nav>
</template>

<script>
export default {
  name: 'PxNav',
}
</script>

<style scoped>
.nav {
  background-color: blue;
}
</style>
