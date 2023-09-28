<template>
    <v-dialog v-model="open_dialog"  persistent > <!-- v-model me permite vincular el v-dialog a una propiedad, en este caso 'open-dialog'-->
      <v-card style="background-color: black;">
        
        <v-card-text >
          
          <div class = "contenedor1"  >
          <p>
            <h2>Name</h2>
            {{ hero.name }}
            <v-img :src="hero.thumbnail.path + '/portrait_incredible.' + hero.thumbnail.extension"  :width="600"/>
          </p>
        </div>
          <div class="contenedor2">

          
          <h2>Description </h2>
          <p>
            {{ hero.description || "Not information available" }}
          </p>
          <h2> Comics</h2>
          <p>
            {{ hero.comics.available || "Not information available"}}
          </p>
          <h2> Series</h2>
          <p>
            {{ hero.series.available || "Not information available"}}
          </p>
          <h2> Stories</h2>
          <p>
            {{ hero.stories.available || "Not information available"}}
          </p>
          <h2> Events</h2>
          <p>
            {{ hero.events.available || "Not information available"}}
          </p>

          <h2> Some series</h2>
          <p v-for="item in hero.series.items.slice(0,3)" :key="item.name" >
            {{ item.name}}
          </p>
        </div>
        </v-card-text>
        <v-card-actions>
          <v-btn color="primary" @click="close_dialog" style="background-color: white; color: black;">Close</v-btn >
        </v-card-actions>
      </v-card>
    </v-dialog>
  </template>

  <!--
    Styles
  -->

  <style>
  v-display {
  font-family: Forte, sans-serif;
}
.contenedor1 {
  color: #f0f0f0;
  background-color: transparent;
  float: left; /* Hace que el primer contenedor flote a la izquierda */
  width: 50%; /* Opcional: ajusta el ancho del contenedor */
  padding: 10px; /* Opcional: añade espacio alrededor del contenido */
  box-sizing: border-box; /* Opcional: incluye el relleno en el ancho total */
}

.contenedor2 {
  color: #f0f0f0;
  background-color: transparent;
  margin-top: 200 px;
  align-items: center;
  float: right; /* Hace que el segundo contenedor flote a la izquierda */
  width: 50%; /* Opcional: ajusta el ancho del contenedor */
  
  padding: 10px; /* Opcional: añade espacio alrededor del contenido */
  box-sizing: border-box; /* Opcional: incluye el relleno en el ancho total */
}


</style>

<script setup>

const open_dialog = ref(false) //declaramos una variable reactiva usando la funcion ref

const hero=ref({})
onBeforeMount(() => {  //funcion que se ejecuta de primerita
    open_dialog.value=props.dialog //la funcion que tenga la pagina que use el componente será transferida a open_dialog
    hero.value=props.hero
});

const props = defineProps({
    dialog: {
        type: Boolean,
        required: true
    },
    hero: {
        type: Object,
        required: true
    }
})

const emit = defineEmits(['close'])   //definimos el evento 'close' que se guarda en la constante emit

const close_dialog = () => { //inicializamos un función flecha que cuando se aprieta el boton close emite el evento close
  // Método para cerrar el diálogo
  emit("close"); // Emite un evento para cerrar el diálogo
}

</script>

  
  