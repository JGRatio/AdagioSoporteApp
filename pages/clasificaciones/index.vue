<template>
  <div>
    <div class="mt-5 mx-5">
      <div class="mt-5 mx-5 card">
        <div class="ml-3 mt-3">
          <h3>Catálogo de Clasificaciones</h3>
          <b-btn variant="primary" class="mb-3" @click="nueva"
            ><b-icon icon="plus"></b-icon> Nueva Clasificación</b-btn
          >
        </div>

        <div class="body px-2">
          <b-table
            hover
            sticky-header="700px"
            :items="list"
            :fields="fields"
            small
          >
            <template #cell(actions)="row">
              <b-dropdown
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
                <b-dropdown-item @click="eliminar(row)">
                  <b-icon icon="trash"></b-icon> Eliminar
                </b-dropdown-item>
              </b-dropdown>
            </template>
          </b-table>
        </div>
      </div>

      <b-modal
        v-model="modalVisible"
        :title="
          clasificacion.IDClasificacion ? 'Editando Clasificacion' : 'Nuevo'
        "
        hide-footer="true"
      >
        <form ref="form">
          <b-form-group
            id="fieldset-codigoclasificacion"
            label="Código"
            label-for="input-codigoclasificacion"
          >
            <b-form-input
              id="input-codigoclasificacion"
              v-model="clasificacion.CodigoClasificacion"
              trim
            ></b-form-input>
          </b-form-group>
          <b-form-group
            id="fieldset-descripcion"
            label="Descripción"
            label-for="input-descripcion"
          >
            <b-form-input
              id="input-descripcion"
              v-model="clasificacion.Descripcion"
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
    <footer class="footerPX">
      <px-footer id="main" />
    </footer>
  </div>
</template>

<script>
import Vue from 'vue'
import { BootstrapVue, BootstrapVueIcons } from 'bootstrap-vue'
import PxFooter from '@/components/PxFooter.vue'

Vue.use(BootstrapVue)
Vue.use(BootstrapVueIcons)

export default {
  name: 'ClasificacionesPage',
  components: { PxFooter },
  async asyncData({ $axios }) {
    const testApis = await $axios.$get(
      'http://localhost:4000/api/v1/clasificaciones/'
    )
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
          key: 'CodigoClasificacion',
          label: 'Código',
          sortable: true,
        },
        {
          key: 'Descripcion',
          label: 'Descripción',
          sortable: false,
        },
      ],
      modalVisible: false,
      clasificacion: {},
    }
  },
  methods: {
    nueva() {
      // this.$router.push({ path: `/clasificaciones/${0}`})
      this.clasificacion = {}
      this.modalVisible = true
    },
    modificar({ item }) {
      // this.$router.push({ path: `/clasificaciones/${item.IDClasificacion}`})
      this.clasificacion = item
      this.modalVisible = true
    },
    async update() {
      const { list } = await this.$axios.$get(
        'http://localhost:4000/api/v1/clasificaciones/'
      )

      this.list = list
    },
    async eliminar({ item }) {
      try {
        await this.$axios.$delete(
          'http://localhost:4000/api/v1/clasificaciones/' + item.IDClasificacion
        )
        this.update()
      } catch (error) {}
    },
    async guardar() {
      try {
        await this.$axios.$post(
          'http://localhost:4000/api/v1/clasificaciones/',
          this.clasificacion
        )
        this.modalVisible = false
        this.update()
      } catch (error) {}
    },
    cancelar() {
      this.modalVisible = false
    },
  },
}
</script>

<style>
.actionsStyle {
  width: 5px;
}
body {
  min-height: 100%;
  top: 0;
  margin: 0;
  padding: 0;
  background-color: #f2f4f8;
}

.tabla {
  height: 700px;
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
</style>
