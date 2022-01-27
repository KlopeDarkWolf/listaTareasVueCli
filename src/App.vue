
<template >
  
  
  <cabecera  @tareaNueva="add"></cabecera>
  <lista-tareas @updateTarea="actualizarLista"  :listado="this.lista">
        <nota></nota>
  </lista-tareas>
</template>

<script>

import nota from './components/nota.vue'
import listaTareas from './components/listaTareas.vue'
import cabecera from './components/cabecera.vue'


export default {
  name: 'App',

  data(){
    return{
      lista:[],
      filtrado:false,
      cadenaFiltrada:null
    }
  },
  components: {
    nota,listaTareas,cabecera
  },
  methods:{
    add(tarea){
      
      this.lista.push(tarea);
      this.ordenarPorPrioridad();
      this.almacenarLocalStorage();
      

    },
    
    actualizarLista(nuevaLista){
      this.lista=nuevaLista;
      this.almacenarLocalStorage();
    },
     almacenarLocalStorage(){
          localStorage.setItem("lista",JSON.stringify(this.lista));
          
        },
        ordenarPorPrioridad(){
          this.lista.sort(function(a,b){
            if(a.prioridad=="baja"&&b.prioridad=="media"){
              return 1;
            }else if(a.prioridad=="baja"&&b.prioridad=="alta"){
              return 1;
            }else if(a.prioridad=="media"&&b.prioridad=="alta"){
              return 1;
            }else if(a.prioridad=="media"&&b.prioridad=="baja"){
              return -1;
            }else if(a.prioridad=="alta"&&b.prioridad=="media"){
              return -1;
            }else if(a.prioridad=="alta"&&b.prioridad=="baja"){
              return -1;
            }
          });
        },

  },
  mounted(){
      if(localStorage.getItem("lista")){
        var datosAlmacenadosEnStorage=JSON.parse(localStorage.getItem("lista"));
        for(let i=0;i<datosAlmacenadosEnStorage.length;i++){
          this.lista.push(datosAlmacenadosEnStorage[i]);
        }
      }
         
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Baloo+Tamma+2:wght@400;500;600;700;800&family=Indie+Flower&display=swap');

/*Establecer la altura de linea, todos los margin y paddings iniciales a 0 y el tamaño de las cajas a border-box*/
*, *::before, *::after {
    
    line-height: 1.8;
     margin: 0;
    padding: 0;
     box-sizing: border-box;
     }

/*Cambiar el tamaño de la letra en la raíz para que sea responsivo*/
:root{
    font-size: 62.5%;
}

/*Estilos para el body y dimensiones*/
body{
    margin: 0;
    font-family: 'Baloo Tamma 2', cursive;
    
}
#app {
  width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
}
</style>
