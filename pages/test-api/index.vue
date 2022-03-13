
<template>
  <div>
    <h3>Catalogo de Clasificaciones</h3>
    <b-btn @click="nueva">NUEVA</b-btn>
     <b-table hover :items="list" :fields="fields">
       <template #cell(actions)="row">
            <div class="d-flex justify-content-center">
                <b-btn  @click="modificar(row)">Modificar</b-btn>
                <b-btn variant="danger" @click="eliminar(row)">Eliminar</b-btn>
            </div>
        </template>

     </b-table>
  </div>
</template>

<script>
export default {
    name: "TestApi",
    async asyncData({ $axios }) {
      const testApis = await $axios.$get('http://localhost:4000/api/v1/clasificaciones/')
      const { list } = testApis;
      return { list }
    },
    data() {
      return {
         fields: [
          {
            key: 'CodigoClasificacion',
            label: 'Codigo',
            sortable: false
          },
          {
            key: 'Descripcion',
            sortable: false
          },
          {
            key: 'actions'
          }
        ],
      }
    },
    methods: {
      nueva() {
        // eslint-disable-next-line no-console
        console.log('HEy')
        this.$router.push({ path: `/test-api/${0}`})
        // this.$router.push({ path: '/pruebas'})
      },
      modificar({item}) { 
        // eslint-disable-next-line no-console
         // console.log(item.IDClasificacion)
        this.$router.push({ path: `/test-api/${item.IDClasificacion}`})
      },
      async update(){
         const {list} = await this.$axios.$get('http://localhost:4000/api/v1/clasificaciones/')
          this.list=list
      }
      ,
      
      async eliminar({item}) { 
        // eslint-disable-next-line no-console
        // console.log({ row })
        try {
          await this.$axios.$delete('http://localhost:4000/api/v1/clasificaciones/'+item.IDClasificacion);
          this.update();
          

        } catch (error) {
            
        }
        
      }
    }
}
</script>

<style>
</style>