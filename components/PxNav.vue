<template>
  <b-nav vertical class="px-2 pt-4 mr-1 pb-5">
    <!-- <b-avatar class="ml-3" src="@/src/images/test.jpg" size="10rem"></b-avatar> -->
    <div class="ml-3">
      <img
        src="@/src/images/Logo_Adagio_fondo_azul.png"
        class="rounded-circle sz"
        alt=""
      />
      <div class="mt-3">
        <b-dropdown-divider></b-dropdown-divider>
        <h3 class="text">Bienvenido</h3>
        <b-nav-item-dropdown
          dropright
          no-caret
          class="text textDecoration nombreUsuario"
        >
          <b-dropdown-header class="font-weight-bold"
            >Opciones de Sesión</b-dropdown-header
          >
          <b-dropdown-divider></b-dropdown-divider>
          <template #button-content>
            <h5>Javier Peña Fuentes</h5>
          </template>
          <b-dropdown-item> Cerrar Sesión </b-dropdown-item>
        </b-nav-item-dropdown>

        <b-dropdown-divider></b-dropdown-divider>
      </div>
    </div>

    <div class="mt-3">
      <b-nav-item-dropdown dropright no-caret>
        <template #button-content>
          <b-icon icon="diagram3-fill"></b-icon> Módulo de Catalogos
        </template>
        <b-dropdown-header class="text-center font-weight-bold"
          >Catalogos</b-dropdown-header
        >
        <b-dropdown-divider></b-dropdown-divider>
        <tr>
          <td>
            <b-dropdown-item>
              <NuxtLink to="/clientes" class="textDecoration">
                <!-- <b-dropdown-item>Clientes</b-dropdown-item> -->
                Clientes
              </NuxtLink>
            </b-dropdown-item>
          </td>
          <td>
            <b-dropdown-item>
              <NuxtLink to="/clasificaciones" class="textDecoration">
                <!-- <b-dropdown-item>Clientes</b-dropdown-item> -->
                Clasificaciones
              </NuxtLink>
            </b-dropdown-item>
          </td>
        </tr>
        <tr>
          <td>
            <b-dropdown-item>
              <NuxtLink to="/dificultades" class="textDecoration">
                <!-- <b-dropdown-item>Clientes</b-dropdown-item> -->
                Dificultades
              </NuxtLink>
            </b-dropdown-item>
          </td>
          <td>
            <b-dropdown-item>
              <NuxtLink to="/especialidades" class="textDecoration">
                Especialidades
              </NuxtLink>
            </b-dropdown-item>
          </td>
        </tr>
      </b-nav-item-dropdown>

      <b-nav-item-dropdown dropright no-caret class="mt-3">
        <template #button-content>
          <b-icon icon="headset"></b-icon> Módulo de Solicitudes
        </template>
        <b-dropdown-header> Solicitudes </b-dropdown-header>
        <b-dropdown-divider></b-dropdown-divider>
        <b-dropdown-item href="#">Panel Principal</b-dropdown-item>
      </b-nav-item-dropdown>

      <b-nav-item-dropdown dropright no-caret class="mt-3">
        <template #button-content>
          <b-icon icon="file-earmark-bar-graph"></b-icon> Módulo de Reportes
        </template>
        <b-dropdown-header> Reportes</b-dropdown-header>
        <b-dropdown-divider></b-dropdown-divider>
        <b-dropdown-item href="#">EN</b-dropdown-item>
      </b-nav-item-dropdown>
      <b-dropdown-divider></b-dropdown-divider>

      <b-nav-item-dropdown dropright no-caret class="mt-3">
        <template #button-content>
          <b-icon icon="gear-fill"></b-icon> Configuración
        </template>
        <b-dropdown-header> Configuración</b-dropdown-header>
        <b-dropdown-divider></b-dropdown-divider>
        <b-dropdown-item href="#">EN</b-dropdown-item>
      </b-nav-item-dropdown>
    </div>
  </b-nav>
</template>

<script>
export default {
  name: 'PxNav',
  data() {
    return {}
  },
}
</script>

<style scoped>
.nav {
  border-right: 1px solid #e3e3e3;
  max-width: 240px;
  height: 100vh;
}

body {
  height: 100%;
}

.sz {
  height: 10rem;
  width: 10rem;
}
.text {
  display: flex;
  align-items: center;
  word-break: break-all;
}
.textDecoration {
  text-decoration: none;
  color: black;
}

#__BVID__222__BV_toggle_ {
  padding: 0rem 0rem !important;
}
/* .textDecoration:hover {
  color: gray;
  background-color: gray;
} */
</style>
