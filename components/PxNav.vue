<template>
  <b-nav vertical class="px-2 pt-4 mr-1 fz-g">
    <!-- <b-avatar class="ml-3" src="@/src/images/test.jpg" size="10rem"></b-avatar> -->
    <div class="ml-3">
      <img
        src="@/src/images/Logo_Adagio_fondo_azul.png"
        class="rounded-circle sz"
        alt=""
      />
      <div class="mt-3">
        <b-dropdown-divider></b-dropdown-divider>
        <b-nav-item>
          <p class="text-wrap textDecoration fz-h3">Bienvenido</p>
        </b-nav-item>

        <b-nav-item-dropdown dropright no-caret class="mt-0">
          <b-dropdown-header class="font-weight-bold"
            >Opciones de Sesión</b-dropdown-header
          >
          <b-dropdown-divider></b-dropdown-divider>
          <template #button-content>
            <p class="text-wrap fz-h4">{{ nombreLogin }}</p>
          </template>
          <b-dropdown-item @click="cerrarSesion">
            Cerrar Sesión
          </b-dropdown-item>
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
        <tr class="fz-g">
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
        <tr class="fz-g">
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
        <tr class="fz-g">
          <td>
            <b-dropdown-item>
              <NuxtLink to="/errores" class="textDecoration">
                <!-- <b-dropdown-item>Clientes</b-dropdown-item> -->
                Errores
              </NuxtLink>
            </b-dropdown-item>
          </td>
          <td>
            <b-dropdown-item>
              <NuxtLink to="/modulos" class="textDecoration">
                Modulos
              </NuxtLink>
            </b-dropdown-item>
          </td>
        </tr>
        <tr class="fz-g">
          <td>
            <b-dropdown-item>
              <NuxtLink to="/oficinas" class="textDecoration">
                <!-- <b-dropdown-item>Clientes</b-dropdown-item> -->
                Oficinas
              </NuxtLink>
            </b-dropdown-item>
          </td>
          <td>
            <b-dropdown-item>
              <NuxtLink to="/perfiles" class="textDecoration">
                Perfiles
              </NuxtLink>
            </b-dropdown-item>
          </td>
        </tr>
        <tr class="fz-g">
          <td>
            <b-dropdown-item>
              <NuxtLink to="/prioridades" class="textDecoration">
                <!-- <b-dropdown-item>Clientes</b-dropdown-item> -->
                Prioridades
              </NuxtLink>
            </b-dropdown-item>
          </td>
          <td>
            <b-dropdown-item>
              <NuxtLink to="/status" class="textDecoration"> Status </NuxtLink>
            </b-dropdown-item>
          </td>
        </tr>
      </b-nav-item-dropdown>

      <b-nav-item-dropdown dropright no-caret class="mt-3">
        <template #button-content>
          <b-icon icon="headset"></b-icon> Módulo de Solicitudes
        </template>
        <b-dropdown-header class="fz-g"> Solicitudes </b-dropdown-header>
        <b-dropdown-divider></b-dropdown-divider>
        <b-dropdown-item class="fz-g">
          <NuxtLink to="/solicitudes" class="textDecoration">
            <!-- <b-dropdown-item>Clientes</b-dropdown-item> -->
            Panel Principal
          </NuxtLink>
        </b-dropdown-item>
      </b-nav-item-dropdown>

      <b-nav-item-dropdown dropright no-caret class="mt-3">
        <template #button-content>
          <b-icon icon="file-earmark-bar-graph"></b-icon> Módulo de Reportes
        </template>
        <b-dropdown-header class="fz-g"> Reportes</b-dropdown-header>
        <b-dropdown-divider></b-dropdown-divider>
        <b-dropdown-item class="fz-g">EN</b-dropdown-item>
      </b-nav-item-dropdown>
      <b-dropdown-divider></b-dropdown-divider>

      <b-nav-item-dropdown dropright no-caret class="mt-3">
        <template #button-content>
          <b-icon icon="gear-fill"></b-icon> Configuración
        </template>
        <b-dropdown-header class="fz-g"> Configuración</b-dropdown-header>
        <b-dropdown-divider></b-dropdown-divider>
        <b-dropdown-item class="fz-g">EN</b-dropdown-item>
      </b-nav-item-dropdown>
    </div>
  </b-nav>
</template>

<script>
// const lll = localStorage.getItem('nombre')
// console.log('cargando')
// console.log(lll)
export default {
  name: 'PxNav',
  data() {
    return {
      nombreLogin: localStorage.getItem('nombre'),
    }
  },
  methods: {
    cerrarSesion() {
      this.$router.push({ path: `/login` })
    },
  },
}
</script>

<style scoped>
.nav {
  border-right: 1px solid #e3e3e3;
  max-width: 240px;
  min-height: 720px;
  height: 100vh;
}

body {
  height: 100%;
}

.sz {
  height: 10rem;
  width: 10rem;
}

.textDecoration {
  text-decoration: none;
  color: black;
}
.fz-g {
  font-size: 13px;
}
.fz-h3 {
  font-size: 22px;
  font-weight: bold;
  margin-bottom: 0;
  padding-bottom: 0;
}
.fz-h4 {
  font-size: 15px;
  margin-top: 0;
  padding-top: 0;
  color: black !important;
}

/* .textDecoration:hover {
  color: gray;
  background-color: gray;
} */
</style>
