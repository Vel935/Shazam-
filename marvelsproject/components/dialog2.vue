<template>
    <v-dialog v-model="open_dialog" max-width="400px" persistent> <!-- v-model me permite vincular el v-dialog a una propiedad, en este caso 'open-dialog'-->
      <v-card>
        <v-card-title></v-card-title>
        <v-card-text v-for="item in hero.comics.items" :key="item.name">
          {{ item.name }}
        </v-card-text>
        <v-card-actions>
          <v-btn color="primary" @click="close_dialog">Close</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </template>

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

  
  