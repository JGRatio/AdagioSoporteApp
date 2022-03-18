<template>
  <div>
    <div class="contenedor">
      <px-nav />
      <div class="cuerpo">
        <main>
          <nuxt />
        </main>
      </div>
    </div>
    <footer class="footerPX">
      <px-footer id="main" />
    </footer>
  </div>
</template>

<script>
import PxNav from '@/components/PxNav.vue'
import PxFooter from '@/components/PxFooter.vue'
export default {
  name: 'LayoutDefault',
  components: { PxFooter, PxNav },
}
</script>

<style>
.actionsStyle {
  width: 5px;
}
body {
  min-height: 720px;
  max-height: 100%;
  top: 0;
  margin: 0;
  padding: 0;
  background-color: #f2f4f8;
}

.footerPX,
section#main,
body {
  width: 100%;
  position: absolute;
}

section#main {
  min-height: 100%;
}

.footerPX {
  bottom: 0;
}

.contenedor {
  display: flex;
  flex-direction: row;
  height: 100vh;
}
.cuerpo {
  flex-grow: 1;
}
</style>
