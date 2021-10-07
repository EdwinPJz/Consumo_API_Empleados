<template>
  <div class="home">
    <Header/>
      
      <div class="container izquierda">
        <button type="button" class="btn btn-primary" v-on:click="nuevo()">Nuevo Empleado</button>
          <table class="table table-hover">
          <thead>
            <tr>
              <th scope="col">ID</th>
              <th scope="col">Código</th>
              <th scope="col">Nombres</th>
              <th scope="col">Apellidos</th>
              <th scope="col">Dirección</th>
              <th scope="col">Teléfono</th>
              <th scope="col">Fecha_Nacimiento</th>
              <th scope="col">Puesto</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="empleado in Listaempleados" :key="empleado.id_empleado" v-on:click="editar(empleado.id_empleado)">
              <th scope="row">{{ empleado.id_empleado }}</th> 
              <td>{{ empleado.codigo }}</td>
              <td>{{ empleado.nombres }}</td>
              <td>{{ empleado.apellidos }}</td>
              <td>{{ empleado.direccion }}</td>
              <td>{{ empleado.telefono }}</td>
              <td>{{ empleado.fecha_nacimiento }}</td>
              <td>{{ empleado.id_puesto }}</td>
            </tr>
           
          </tbody>
        </table>
      </div>
    <Footer/>
  </div>
</template>

<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import axios from 'axios';
  export default {
    name: 'Home',
    data(){
      return {
        Listaempleados:null,
        pagina:1
      }
    },
    components: {
      Header,
      Footer
    },
    methods:{
      editar(id){
        this.$router.push('/editar/' + id);
      },
      nuevo(){
        this.$router.push('/nuevo');
      }
    },
    mounted:function(){
      let direccion = "https://localhost:5001/api/employee";
      axios.get(direccion).then( data =>{
        this.Listaempleados = data.data;
      });
    }
  }
</script>

<style scoped>
  .izquierda{
    text-align: left;
  }
</style>