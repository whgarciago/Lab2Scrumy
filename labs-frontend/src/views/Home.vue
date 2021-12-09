<template>
  <div class="container-fluid mt-2">
    <h1>Bienvenido</h1>
    <div class="row">
        
        <div class="container-fluid row justify-content-around">
          <div class="col-4">
            <button v-on:click= "mostrarCursos" class="offset-sm-1 offset-md-2 btn btn-primary">
                    Mostrar cursos
            </button>
          </div>
          <div class="col-4">
            <button v-on:click= "mostrarRoles" class="offset-sm-1 offset-md-2 btn btn-primary">
                        Mostrar Roles
            </button>
          </div>
          <div class="col-4">
            <button v-on:click= "agregarRol" class="offset-sm-1 offset-md-2 btn btn-primary">
                    Agregar Rol
            </button>
          </div>
        </div>
        <router-view></router-view>       
    </div> 
  </div>
</template>

<script>
  import axios from 'axios';
  import {getAuthenticationToken} from '@/dataStorage';
  const requestPath = '/roles';

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
      axios.get( this.$store.state.backURL + requestPath, { params: { access_token: getAuthenticationToken( ) } } )
        .then( response => {
          if( response.status !== 200 ){
            alert( 'Error Obteniendo sus roles' );
          }else{
            this.roles = response.data;
            console.log(this.roles)
          }
        } ).catch( error => {
          alert( 'Error en la petición' );
          console.log( error );
        } );
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
      }
    }
  }
</script>

<style>

</style>
