<template>
  <div class="mt-5 mx-5">
    <div class="mt-5 mx-5 card">
      <div class="ml-3 mt-3">
        <h3>Catalogo de Clasificaciones</h3>
        <b-btn variant="primary" class="mb-3" @click="nueva"
          ><b-icon icon="plus"></b-icon> Nueva Clasificación</b-btn
        >
      </div>

      <div class="body px-2">
        <b-table hover :items="list" :fields="fields" small>
          <template #cell(actions)="row">
            <b-dropdown toggle-class="text-decoration-none" no-caret size="sm">
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
          label="Descripcion"
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
</template>

<script>
export default {
  name: 'ClasificacionesPage',
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
          class: 'actions',
        },
        {
          key: 'CodigoClasificacion',
          label: 'Código',
          sortable: false,
        },
        {
          key: 'Descripcion',
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
.actions {
  width: 5px;
}
</style>
