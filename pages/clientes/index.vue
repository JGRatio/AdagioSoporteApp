<template>
  <div class="card px-5 mx-3 mt-4">
    <!-- HEADER DE CATALOGO -->
    <div class="pt-2">
      <h3>Catálogo de Clientes</h3>
      <b-btn variant="primary" class="mb-3" @click="nueva"
        ><b-icon icon="plus"></b-icon> Nuevo Cliente</b-btn
      >
    </div>
    <!-- TABLA -->
    <div class="body">
      <b-table hover sticky-header="70vh" :items="list" :fields="fields" small>
        <template #cell(actions)="row">
          <b-dropdown
            dropright
            toggle-class="text-decoration-none"
            no-caret
            size="sm"
          >
            <template #button-content>
              <b-icon icon="list"></b-icon>
            </template>

            <b-dropdown-item @click="modificar(row)">
              <b-icon icon="blockquote-right"></b-icon> Modificar
            </b-dropdown-item>
            <b-dropdown-item @click="confirmarEliminar(row)">
              <b-icon icon="trash"></b-icon> Eliminar
            </b-dropdown-item>
          </b-dropdown>
        </template>
      </b-table>
    </div>

    <b-modal
      v-model="modalVisible"
      :title="cliente.IDCliente ? 'Editando Cliente' : 'Nuevo'"
      hide-footer="true"
    >
      <form ref="form">
        <b-form-group
          id="fieldset-codigocliente"
          label="Código"
          label-for="input-codigocliente"
        >
          <b-form-input
            id="input-codigocliente"
            v-model="cliente.CodigoCliente"
            trim
          ></b-form-input>
        </b-form-group>
        <b-form-group
          id="fieldset-nombrecomercial"
          label="Nombre Comercial"
          label-for="input-nombrecomercial"
        >
          <b-form-input
            id="input-nombrecomercial"
            v-model="cliente.NombreComercial"
            trim
          ></b-form-input>
        </b-form-group>
        <b-form-group
          id="fieldset-urlsitio"
          label="URL Sitio"
          label-for="input-urlsitio"
        >
          <b-form-input
            id="input-urlsitio"
            v-model="cliente.URLSitio"
            trim
          ></b-form-input>
        </b-form-group>
      </form>

      <footer class="modal-footer">
        <b-button class="mt-2" variant="primary" @click="guardar"
          >Guardar</b-button
        >
        <b-button class="mt-2" variant="danger" @click="cancelar"
          >Cancelar</b-button
        >
      </footer>
    </b-modal>
  </div>
</template>

<script>
import Vue from 'vue'
import { BootstrapVue, BootstrapVueIcons } from 'bootstrap-vue'
import VueSweetalert2 from 'vue-sweetalert2'
import 'sweetalert2/dist/sweetalert2.min.css'

Vue.use(BootstrapVue)
Vue.use(BootstrapVueIcons)
Vue.use(VueSweetalert2)

export default {
  name: 'ClientesPage',
  layout: 'navFooter',
  async asyncData({ $axios }) {
    const testApis = await $axios.$get('/clientes/')
    const { list } = testApis
    return { list }
  },
  data() {
    return {
      fields: [
        {
          key: 'actions',
          label: '',
          class: 'actionsStyle',
        },
        {
          key: 'CodigoCliente',
          label: 'Código',
          sortable: true,
        },
        {
          key: 'NombreComercial',
          label: 'Nombre Comercial',
          sortable: false,
        },
        {
          key: 'URLSitio',
          label: 'URL',
          sortable: false,
        },
      ],
      modalVisible: false,
      cliente: {},
    }
  },
  methods: {
    nueva() {
      this.cliente = {}
      this.modalVisible = true
    },
    modificar({ item }) {
      this.cliente = item
      this.modalVisible = true
    },
    async update() {
      const { list } = await this.$axios.$get('/clientes/')

      this.list = list
    },
    async eliminar({ item }) {
      try {
        await this.$axios.$delete('/clientes/' + item.IDCliente)
        this.update()
      } catch (error) {}
    },
    async guardar() {
      try {
        await this.$axios.$post('/clientes/', this.cliente)
        this.modalVisible = false
        this.update()
      } catch (error) {}
    },
    cancelar() {
      this.modalVisible = false
    },
    confirmarEliminar(row) {
      this.$swal
        .fire({
          title: '¿Deseas eliminar este registro?',
          text: 'Esta acción no se puede revertir',
          icon: 'warning',
          showCancelButton: true,
          confirmButtonColor: '#3085d6',
          cancelButtonColor: '#d33',
          confirmButtonText: 'Eliminar',
        })
        .then((result) => {
          if (result.isConfirmed) {
            this.$swal.fire(
              'Eliminado',
              'El registro ha sido eliminado',
              'success'
            )
            this.eliminar(row)
          }
        })
    },
  },
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