<template>
  <div class="container-fluid mt-2">
    <h1>Bienvenido</h1>
    <div class="row">
        
        <div class="container-fluid row justify-content-around col-12">
            <button v-on:click= "mostrarCursos" class="offset-sm-1 offset-md-2 btn btn-primary">
                    Mostrar cursos
            </button>
          
            <button v-on:click= "mostrarRoles" class="offset-sm-1 offset-md-2 btn btn-primary">
                        Mostrar Roles
            </button>
            <button v-on:click= "agregarRol" class="offset-sm-1 offset-md-2 btn btn-primary">
                    Agregar Rol
            </button>
            <button v-on:click= "crearCurso" class="offset-sm-1 offset-md-2 btn btn-primary">
                    Crear Curso
            </button>
        </div>
        <router-view></router-view>       
    </div> 
  </div>
</template>

<script>
  import {getAuthenticationToken} from '@/dataStorage';

  export default{

    name: "Home",

    data( ){
      return{
        names: '',
        surnames: '',
        username: '',
        password: '',
        cPassword: '',
        role: '',
        roles: [{id: 1, roleName: 'My Role'}],
        response: null
      }
    },

    beforeCreate( ){
      if( !getAuthenticationToken( ) ){
        this.$router.push( {name: 'login'} )
      }
    },

    methods:{
      mostrarCursos(){
        this.$router.push( {name: 'courses'} )
      },
      mostrarRoles(){
        this.$router.push({ name: 'roles'} )
      },
      agregarRol(){
        this.$router.push({ name: 'add-role'} )
      },
      crearCurso(){
        this.$router.push({ name: 'crear-curso'} )
      }
    }
  }
</script>

<style>

</style>
