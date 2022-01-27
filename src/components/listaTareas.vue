<template>
                <div id="listado">
                  <h2 >Lista de Tareas</h2>
                 <div  class="listado_tareas">
                   
                  <nota v-for="(tarea,index) in listaComputada" @borrarTarea="borrarTarea" @activarTarea="cambioEstadoTarea" @cambiarPrioridadDeTarea="cambioPrio" :key="index" :posicion="index" :tarea="tarea"  ></nota>
                 </div>

                <span>Tienes {{lista.length}} tareas, {{numeroDeTareasCompletadas}} están completadas</span>
                <a v-bind:class="{listaSeleccionada:this.tareasCompletadas}" v-on:click="mostrarCompletadas()" >Mostrar completadas</a> <a v-bind:class="{listaSeleccionada:this.tareasActivas}" v-on:click="mostrarActivas()">Mostrar activas</a> <a v-bind:class="{listaSeleccionada:this.todasTareas}" v-on:click="mostrarTodas()">Mostrar Todos</a>
                <a v-on:click="borrarCompletadas()">Borrar Completadas</a>
                </div>
                
</template>

<script>

import nota from './nota.vue'

export default {
  name: 'listaTareas',
  props: {
    listado:null
  },
  data() {
      return{
        lista:this.listado,
        todasTareas:true,
        tareasCompletadas:false,
        tareasActivas:false,

        
      }
  },

  components:{
    nota
  },
  methods:{
    cambioPrio(index,prioridad){
      this.lista[index].prioridad=prioridad;
      this.ordenarPorPrioridad();
      this.$emit("updateTarea",this.lista);
    },
    cambioEstadoTarea(index,estado){
      this.lista[index].activa=estado;
      this.$emit("updateTarea",this.lista);
    },
    borrarTarea(index){
      this.lista.splice(index,1);
      this.$emit("updateTarea",this.lista);
    },
    
      mostrarCompletadas(){
          this.tareasCompletadas=true;
          this.todasTareas=false;
          this.tareasActivas=false;
         
        },

        mostrarActivas(){
          this.tareasCompletadas=false;
          this.todasTareas=false;
          this.tareasActivas=true;
         
        },

        mostrarTodas(){
          this.tareasCompletadas=false;
          this.todasTareas=true;
          this.tareasActivas=false;
          
        },
        borrarCompletadas(){
          
          this.lista=this.lista.filter(tarea=>tarea.activa);
          this.$emit("updateTarea",this.lista);
          
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
        }
  },
  computed:{
    listaComputada(){
        var listaFiltrada=this.lista;
        if(this.tareasCompletadas){
          listaFiltrada=this.lista.filter(tarea=>!tarea.activa);
        }else if(this.tareasActivas){
          listaFiltrada=this.lista.filter(tarea=>tarea.activa);
        }
        return listaFiltrada;
      },
    
    
    numeroDeTareasCompletadas(){
        var numeroDeTareasCompletadas=this.lista.filter(tarea=>!tarea.activa).length;
        return numeroDeTareasCompletadas;
      }
  
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/*Dar estilos al conetenedor de las tareas*/
#listado{
    width: 60%;
    border: 0.1rem solid black;
    border-radius: 0.7rem;
    background-color: #ebecf0;
}
/*Dar tamaño, borde y posición a la cabecera de la lista de tareas*/
#listado h2{
    text-align: center;
    font-size: 3rem;
    border-bottom: 0.1rem solid black;
    
}


.listado_tareas{
    display: flex;
    justify-content: space-between;
    flex-direction: column;
    border-bottom: 0.1rem solid black;
    padding-top: 2rem;
    
}

.listado_tareas nota{
  display: flex;
  flex-direction: row;
  width: 100%;
}

.listado_tareas h3{
    width: 20%;
}

span,a{
  font-size: 2rem;
  padding: 1.5rem;
}
a{
  cursor: pointer;
}
.listaSeleccionada{
  color: rgb(20, 122, 206);
  font-weight: bold;
}
</style>
