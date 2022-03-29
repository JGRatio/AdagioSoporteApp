<template>
  <div class="px-2 mx-3 mt-3">
    <!-- HEADER-->
    <div class="pt-4 pb-4 px-3 mb-5 card">
      <h3>Modulo de Solicitudes</h3>
    </div>

    <div class="body card">
      <!-- FILTROS -->
      <div class="pt-2 pb-2 px-3 mb-5">
        <h4>Filtros</h4>
        <div class="border-bottom mt-3"></div>
        <div class="mt-2 contenderoFiltros">
          <div class="filtro">
            Agente
            <v-select
              v-model="selected.selectedAgente"
              label="text"
              multiple
              :placeholder="tagPlaceHolder"
              :options="options.optionsAgente"
              class="sizeBox"
            />
          </div>
          <div class="filtro">
            Cliente
            <v-select
              v-model="selected.selectedCliente"
              label="text"
              multiple
              :placeholder="tagPlaceHolder"
              :options="options.optionsClientes"
              class="sizeBox"
            />
          </div>
          <div class="filtro">
            Status
            <v-select
              v-model="selected.selectedStatus"
              label="text"
              multiple
              :placeholder="tagPlaceHolder"
              :options="options.optionsStatus"
              class="sizeBox"
            />
          </div>
          <div class="filtro">
            Modulo
            <v-select
              v-model="selected.selectedModulo"
              label="text"
              multiple
              :placeholder="tagPlaceHolder"
              :options="options.optionsModulo"
              class="sizeBox"
            />
          </div>
          <div class="filtro">
            Clasificación
            <v-select
              v-model="selected.selectedClasificacion"
              label="text"
              multiple
              :placeholder="tagPlaceHolder"
              :options="options.optionsClasificacion"
              class="sizeBox"
            />
          </div>
          <div class="filtro">
            Prioridad
            <v-select
              v-model="selected.selectedPrioridad"
              label="text"
              multiple
              :placeholder="tagPlaceHolder"
              :options="options.optionsPrioridad"
              class="sizeBox"
            />
          </div>
          <div class="filtro">
            Fecha Inicial
            <b-input-group>
              <b-form-input
                id="fechaini-input"
                v-model="selected.selectedFechaIni"
                type="text"
                placeholder="YYYY-MM-DD"
                autocomplete="off"
              ></b-form-input>
              <b-input-group-append>
                <b-form-datepicker
                  v-model="selected.selectedFechaIni"
                  button-only
                  right
                  aria-controls="fechaini-input"
                  @context="onContext"
                ></b-form-datepicker>
              </b-input-group-append>
            </b-input-group>
          </div>
          <div class="filtro">
            Fecha Final
            <b-input-group>
              <b-form-input
                id="fechafin-input"
                v-model="selected.selectedFechaFin"
                type="text"
                placeholder="YYYY-MM-DD"
                autocomplete="off"
              ></b-form-input>
              <b-input-group-append>
                <b-form-datepicker
                  v-model="selected.selectedFechaFin"
                  button-only
                  right
                  aria-controls="fechafin-input"
                  @context="onContext"
                ></b-form-datepicker>
              </b-input-group-append>
            </b-input-group>
          </div>
        </div>

        <b-btn variant="primary" class="mt-3" @click="filtrar"
          ><b-icon icon="filter"></b-icon> Filtrar</b-btn
        >
        <b-btn variant="light" class="mt-3" @click="limpiarFiltros"
          ><b-icon icon="filter"></b-icon> Limpiar Filtros</b-btn
        >

        <div class="border-bottom mt-5"></div>
      </div>

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
import vSelect from 'vue-select'
import 'vue-select/dist/vue-select.css'

Vue.component('VSelect', vSelect)

Vue.use(BootstrapVue)
Vue.use(BootstrapVueIcons)
Vue.use(VueSweetalert2)

export default {
  name: 'SolicitudesPage',
  layout: 'navFooter',
  async asyncData({ $axios }) {
    const selected = {
      selectedTicket: [],
      selectedCliente: [],
      selectedAgente: [],
      selectedStatus: [],
      selectedModulo: [],
      selectedClasificacion: [],
      selectedPrioridad: [],
      selectedFechaIni: null,
      selectedFechaFin: null,
    }

    const token = localStorage.getItem('token')
    $axios.defaults.headers.common['token-auth'] = token

    const params = JSON.stringify(selected)

    const testApis = await $axios.$get('/solicitudes/', {
      params,
    })

    const { list } = testApis
    // delete $axios.defaults.headers.common['token-auth']
    return { list }
  },
  data() {
    return {
      selected: {
        selectedTicket: [],
        selectedCliente: [],
        selectedAgente: [],
        selectedStatus: [],
        selectedModulo: [],
        selectedClasificacion: [],
        selectedPrioridad: [],
        selectedFechaIni: null,
        selectedFechaFin: null,
      },

      options: {
        optionsClientes: [],
        optionsStatus: [],
        optionsModulo: [],
        optionsClasificacion: [],
        optionsPrioridad: [],
      },

      fields: [
        {
          key: 'actions',
          label: '',
          class: 'actionsStyle',
        },
        {
          key: 'IDTicket',
          label: 'Folio Ticket',
          sortable: true,
        },
        {
          key: 'AGENTE',
          label: 'Agente',
          sortable: false,
        },
        {
          key: 'USUARIO',
          label: 'Usuario',
          sortable: false,
        },
        {
          key: 'CLIENTE',
          label: 'Cliente',
          sortable: false,
        },
        {
          key: 'DIFICULTAD',
          label: 'Dificultad',
          sortable: false,
        },
        {
          key: 'PRIORIDAD',
          label: 'Prioridad',
          sortable: false,
        },
        {
          key: 'MODULO',
          label: 'Modulo',
          sortable: false,
        },
        {
          key: 'STATUS',
          label: 'Status',
          sortable: false,
        },
        {
          key: 'ERROR',
          label: 'Error',
          sortable: false,
        },
        {
          key: 'CLASIFICACION',
          label: 'Clasificacion',
          sortable: false,
        },
        {
          key: 'Duracion',
          label: 'Duracion',
          sortable: false,
        },
        {
          key: 'DuracionAgente',
          label: 'Duracion Agente',
          sortable: false,
        },
        {
          key: 'URLTrello',
          label: 'URLTrello',
          sortable: false,
        },
        {
          key: 'Fecha',
          label: 'Fecha',
          sortable: false,
        },
      ],
      modalVisible: false,
      cliente: {},
      tagPlaceHolder: 'Seleccione una opción',
    }
  },

  async mounted() {
    // const { list } = await this.$axios.$get('/clientes/')
    const cliente = await this.$axios.$get('/clientes/')
    const status = await this.$axios.$get('/status/')
    const modulo = await this.$axios.$get('/modulos/')
    const clasificacion = await this.$axios.$get('/clasificaciones/')
    const prioridades = await this.$axios.$get('/prioridades/')
    const listaClientes = cliente.list
    const listaStatus = status.list
    const listaModulos = modulo.list
    const listaClasificacion = clasificacion.list
    const listaPrioridades = prioridades.list
    listaClientes.forEach((element) => {
      this.options.optionsClientes.push({
        value: element.IDCliente,
        text: element.NombreComercial,
      })
    })
    listaStatus.forEach((element) => {
      this.options.optionsStatus.push({
        value: element.IDStatus,
        text: element.Descripcion,
      })
    })
    listaModulos.forEach((element) => {
      this.options.optionsModulo.push({
        value: element.IDModulo,
        text: element.Descripcion,
      })
    })
    listaClasificacion.forEach((element) => {
      this.options.optionsClasificacion.push({
        value: element.IDClasificacion,
        text: element.Descripcion,
      })
    })
    listaPrioridades.forEach((element) => {
      this.options.optionsPrioridad.push({
        value: element.IDPrioridad,
        text: element.Descripcion,
      })
    })
  },
  methods: {
    async limpiarFiltros() {
      this.selected.selectedCliente = []
      this.selected.selectedStatus = []
      this.selected.selectedModulo = []
      this.selected.selectedClasificacion = []
      this.selected.selectedPrioridad = []
      this.selected.selectedFechaIni = null
      this.selected.selectedFechaFin = null

      const selected = {
        selectedTicket: [],
        selectedCliente: [],
        selectedAgente: [],
        selectedStatus: [],
        selectedModulo: [],
        selectedClasificacion: [],
        selectedPrioridad: [],
        selectedFechaIni: null,
        selectedFechaFin: null,
      }

      const params = JSON.stringify(selected)
      const { list } = await this.$axios.$get('/solicitudes/', {
        params,
      })
      this.list = list
    },
    async update() {
      const params = JSON.stringify(this.selected)
      const { list } = await this.$axios.$get('/solicitudes/', {
        params,
      })
      // const { list } = await this.$axios.$get('/solicitudes/', this.selected)

      this.list = list
    },

    filtrar() {
      this.update()
    },
    nueva() {
      this.cliente = {}
      this.modalVisible = true
    },
    modificar({ item }) {
      this.cliente = item
      this.modalVisible = true
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
.contenderoFiltros {
  display: flex;
  flex-wrap: wrap;
  /* justify-content: space-between; */
}
.filtro {
  margin-top: 5px;
  margin-right: 15px;
  width: 240px;
}
</style>
