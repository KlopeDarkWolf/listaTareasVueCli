<template>

            <header>
            <h1>Tasks Map</h1>
            
            
            <div id="search">
                
                <input v-model="nuevaTarea" v-on:keyup.enter="addTarea" type="text" placeholder="Descripción de la tarea">
                
                
            </div>
            
            <div id="prioridad">
                <input id="baja" v-model="prioridad" type="radio" name="prioridad" value="baja" > 
                <label for="baja">Baja</label>

                <input id="media" v-model="prioridad" type="radio" name="prioridad" value="media" > 
                <label for="media">Media</label>

                <input id="alta" v-model="prioridad" type="radio" name="prioridad" value="alta" > 
                <label for="alta">Alta</label>
                 
              </div>
           
            
        </header>
                
</template>

<script>



export default {
  name: 'cabecera',
  props: {
    
  },
  data() {
      return{
        prioridad:"",
        nuevaTarea:"",

        
      }
  },
  emits:['tareaNueva']
  ,
  components:{
    
  },
  methods:{
    addTarea(){
    var fechaAct=Date.now();
    var objeto={nombre:this.nuevaTarea,fecha:fechaAct,prioridad:this.prioridad,activa:true};
    if(objeto.prioridad!=""){
        this.$emit("tareaNueva",objeto);
    }
    
    }
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/*Dimensionar header, añadirle imagen de fondo, color al texto incluido y posicionar sus elementos con Flexbox*/
header{
    width: 100vw;
    background-image:url("../assets/fondoMenu.jpg");
    background-repeat: no-repeat;
    background-size: cover;
    color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 5rem;
    

}
/*Dimensionar el título de la cabecera*/
header h1{
    font-size: 10rem;
    
    margin-top: 5rem;
    margin-bottom: 0;
    
}
/*Dimensionar el buscador, darle estilos y posicionar sus elementos*/
#search{
    background-color: white;
    width: 20%;
    height: 5rem;
    border: 0.1rem solid black;
    border-radius: 10rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
    
}
/*Dimensionar y dar estilos al input de búsqueda*/
#search input{
    margin-left: 1rem;
    width: 80%;
    height: 85%;
    border: none;
}
/*Dimensionar el icono de búsqueda y darle color*/
#search i{
    width: 10%;
    color: black;
    cursor: pointer;
}

/*Dimensionar y dar estilos al selector de prioridades*/
#prioridad{
    border: 0.1rem solid white;
    font-size: 2.5rem;
    display: flex;
    align-items: center;
    margin-bottom: 8vh;
}
/*Ocultar el input radio estándar para reemplazarlo por uno con estilos*/
#prioridad input{
    display: none;
    margin-right: 2rem;
    height: 3rem;
    width: 4rem;
    
    
    
}
/*Dimensionar el label para que este nos sirva de contenedor para el input radio modificado*/
#prioridad label{
    display: inline-block;
    padding: 0.5rem 1.5rem 0.5rem 5.1rem;
    position: relative;
    cursor: pointer;
    
}
/*Generar el input radio modificado detrás del label*/
#prioridad label:before{
    content: "";
    width: 1.7rem;
    height: 1.7rem;
    display: inline-block;
    background: none;
    border:0.3rem solid white;
    border-radius: 50%;
    position: absolute;
    left: 1.7rem;
    top: 1.7rem;
    
}
/*Animación al seleccionar el input radio correspondiente*/
#prioridad input[type="radio"]:checked+label{
    padding: 0.5rem 1.5rem;
    background:rgb(128, 32, 197);
    border-radius:0.2rem;
    color: white;
    transition: all ease 2s;
}
/*Ocultar el input radio modificado*/
#prioridad input[type="radio"]:checked+label:before{
    display: none;
}
</style>
