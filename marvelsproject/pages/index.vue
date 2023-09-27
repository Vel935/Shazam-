<template>
    <div class= "mt-3">
      <h1>Personajes de Marvel</h1>
      
        
        
            <v-container >
            <v-row >
            <v-col v-for="item in personajes" :key="item.id" cols = "2" row = "2">
            
            
              <v-img :src="item.thumbnail.path + '/portrait_fantastic.' + item.thumbnail.extension" />
            
              {{ item.name }}
            <v-btn  @click="openDialog(item.id)" > Ver mas info</v-btn>
            </v-col>
            </v-row>
            </v-container>
               
    </div>
    <dialog2 v-if="open_dialog" :dialog="open_dialog" :hero="heroeunico" @close="cerrar" />
  </template>
<script setup>
import axios from "axios";
const personajes = ref({});
const open_dialog = ref(false); // Definimos open_dialog 
const heroeunico = ref({});

onBeforeMount(() => {
  loadcharacters();
});

const loadcharacters = async () => {
  const url = "https://gateway.marvel.com/v1/public/characters?ts=1&apikey=713c10c5e2edcc62bec72bc4676d723e&hash=e83333736a62ebe7c59b553f42434f4b";
  const { data } = await axios.get(url);
  personajes.value = data.data.results;
  console.log(personajes.value);
};

const openDialog = (id_hero) => {
  open_dialog.value = true;
  heroeunico.value = personajes.value.find(hero => hero.id === id_hero);
  console.log(heroeunico.value);
};

const cerrar = () => {
  console.log("Hola")
  open_dialog.value = false;
};
</script>
