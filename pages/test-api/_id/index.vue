<template>
  <div>
      <h2>{{ item.IDClasificacion ? 'Editando Clasificacion' : 'Nuevo' }}</h2>
      <b-container fluid>
        <b-row>
            <b-col>
                <b-form-group
                    id="fieldset-codigoclasificacion"
                    label="Código"
                    label-for="input-codigoclasificacion"
                >
                    <b-form-input id="input-codigoclasificacion" v-model="item.CodigoClasificacion" trim></b-form-input>
                </b-form-group>
            </b-col>
            <b-col>
                <b-form-group 
                    id="fieldset-descripcion"
                    label="Descripcion"
                    label-for="input-descripcion">
                    <b-form-input id="input-descripcion" v-model="item.Descripcion" trim></b-form-input>
                </b-form-group>
            </b-col>
        </b-row>
        <b-row>
            <b-col style="display:flex; justify-content: flex-end;">
                <b-btn variant="primary" @click="guardar">
                    Guardar
                </b-btn>
                <b-btn variant="info" @click="cancelar">
                    Cancelar
                </b-btn>
            </b-col>
        </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
    name: "ClasificacionesForm",
     async asyncData({ $axios, params }) {
        let item = {
            IDClasificacion: null,
            CodigoClasificacion: null,
            Descripcion: null
            
        }
        if (params.id === '0') return { item }
      const response = await $axios.$get('http://localhost:4000/api/v1/clasificaciones/'+params.id)
      item = response.item;
      return { item }
    },
    data() {
        return {}
    },
    computed: {
        Id() {
            // eslint-disable-next-line no-console
            // console.log(this.$route.params)
            return this.$route.params.id
        }
    },
    methods: {
        async guardar() {
            try {
                
                await this.$axios.$post('http://localhost:4000/api/v1/clasificaciones/', this.item);
                this.$router.push({ path: '/test-api' })
            } catch (error) {
                
            } 
        },
        cancelar() {
            this.$router.push({ path: '/test-api' })
        }
    }
    
}
</script>

<style>
</style>