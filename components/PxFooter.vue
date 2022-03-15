<template>
  <div>
    <footer class="adgPiePagina">
      <div class="adgPiePagina-content border-top-3">
        <p class="pull-right">
          <label>Powered by</label>
          <a href="//adagio.com.mx" target="_blank"
            ><img
              alt=""
              src="@/src/images/adagio-logo.png?p=39387"
              style="width: 75px; height: 20px" /></a
          ><br />
        </p>
        <p class="pull-left">
          <label>©2022 ADAGIO - Todos los derechos reservados</label>
          <label>Versión 1.0.0</label>
        </p>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'PxFooter',
}
</script>

<style scoped>
.adgPiePagina-content {
  padding-top: 10px;
  height: 50px;
  width: 100%;
  font-size: 13px;
  color: #aeb7c5;
  display: inline-block;
}

.adgPiePagina {
  border: 1px solid #dee2e6 !important;
  border-top-color: #dee2e6;
  width: 100%;
  background-color: #fff;
  padding-left: 20px;
  padding-right: 20px;
  padding-bottom: 0;

  bottom: 0;
}
.pull-right {
  float: right;
}
.pull-left {
  float: left;
}
</style>
