<template>
  <!-- CONTENEDOR PRINCIPAL -->
  <div class="row mb-0">
    <!-- FORM LOGIN -->
    <div class="text-center mt-5 mx-5 col" cz-shortcut-listen="true">
      <div class="form-signin mx-5">
        <!-- <img class="mb-4" src="@/src/images/logo.jpg" alt="" width="150" height="150"> -->

        <!-- LOGO ADAGIO -->
        <b-avatar
          class="mb-4"
          src="@/src/images/logo.jpg"
          size="10rem"
        ></b-avatar>
        <h1 class="">¡Hola bienvenido!</h1>
        <p><em>Inicia Sesión para comenzar</em></p>
        <div class="mx-5">
          <!-- <label for="inputEmail" class="sr-only">Email address</label> -->
          <input
            id="input-Email"
            v-model="datos.Correo"
            type="email"
            class="form-control mx-2"
            placeholder="Correo electrónico"
            required=""
            autofocus=""
          />
          <!-- <label for="inputPassword" class="sr-only">Password</label> -->
          <input
            id="input-Password"
            v-model="datos.Password"
            type="password"
            class="form-control mt-2 mx-2"
            placeholder="Contraseña"
            required=""
          />
          <div class="checkbox mb-3 mt-3">
            <label>
              <input type="checkbox" value="remember-me" /> Recuérdame
            </label>
          </div>
        </div>
        <div class="row">
          <div class="col"></div>
          <button
            class="btn btn-lg btn-primary btn-block col"
            type="submit"
            @click="validacion"
          >
            Acceder
          </button>
          <div class="col"></div>
        </div>

        <p class="mt-5 mb-3 text-muted">© 2022</p>
      </div>
    </div>
    <!-- IMAGEN LADO IZQUIERDO -->
    <div class="col">
      <img
        src="@/src/images/loginBackground.jpg"
        class="accounts-image__overlay"
        alt="Responsive image"
      />
      <!-- <px-carousel class="accounts-image__overlay"/> -->
    </div>
  </div>
</template>

<script>
// import PxCarousel from "@/components/PxCarousel.vue"

export default {
  name: 'PxLogin',
  //   components: { PxCarousel }
  data() {
    return {
      datos: {},
    }
  },
  methods: {
    async validacion() {
      try {
        console.log(this.datos)
        const { item } = await this.$axios.$post('/login', this.datos)
        if (item === 1) console.log('Si existe')
        else console.log('No existe')
      } catch (error) {}
    },
  },
}
</script>

<style scoped>
.accounts-image__overlay {
  position: absolute;
  top: 0;

  height: 100vh;

  display: grid;
  grid-template-rows: 1fr 1fr;
}
</style>
