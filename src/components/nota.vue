<template>
              <div id="nota">
                <input id="check1" v-if="tarea.activa"  @click="completarTarea()" type="checkbox" >
                <input id="check2" v-else @click="completarTarea()" type="checkbox" checked>
                
                <h3 v-bind:class="{activa:!tarea.activa}">{{tarea.nombre}}</h3>
                <p>{{Math.floor((Date.now()-tarea.fecha)/60000)}}m</p>
                <p>Prioridad {{tarea.prioridad}}</p>
                <p>{{tarea.activa}}</p>
                <select v-model="prioridad">
                  <option value="alta">alta</option>
                  <option value="media">media</option>
                  <option value="baja">baja</option>
                </select>
                
                
                <button id="cambiarPrio" @click="cambiarPrioridad()" >Cambiar Prioridad</button>
                <button id="borrar" @click="borrarTarea()">Borrar Tarea</button>
            </div>
                
</template>

<script>
export default {
  name: 'nota',
  props: {
    tarea:null,
    posicion:Number

  },
  emits:['cambiarPrioridadDeTarea','activarTarea','borrarTarea']

  ,
  data() {
      return{
        prioridad:"alta" 
      }
  },
  methods:{
    cambiarPrioridad(){
      
          this.$emit("cambiarPrioridadDeTarea",this.posicion,this.prioridad);
          
        },
    
    completarTarea(){
          var estadoDeActivacion=!this.tarea.activa;
          this.$emit("activarTarea",this.posicion,estadoDeActivacion);
          
        },
    borrarTarea(){
          this.$emit("borrarTarea",this.posicion);
        }
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    #nota{
      display: flex;
      width: 100%;
      font-size: 1.5rem;
      justify-content: space-around;
      margin-bottom: 2rem;
    }

    #nota h3{
      width: 30%;
    }

    #nota select{
      height: min-content;
      padding: 0.5rem;
    }

    #nota button#borrar{
      height: min-content;
      padding: 0.5rem;
      background-color: red;
      border-radius: 10%;
      color: white;
    }

    #nota button#cambiarPrio{
      height: min-content;
      padding: 0.5rem;
      background-color: rgb(93, 23, 185);
      border-radius: 10%;
      color: white;
    }

    .activa {
		text-decoration: line-through;
    color: grey;
	}

	

</style>
