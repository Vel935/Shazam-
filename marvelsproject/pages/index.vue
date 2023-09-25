<template>
    <div class= "mt-3">
      <h1>Personajes de Marvel</h1>
      <v-table>
        <thead>
                <tr>
                    <th class="text-left">
                        Nombre
                    </th>
                </tr>
            </thead>
        <tbody>
            <tr v-for="item in personajes" :key="item.id">
            <td>{{ item.name }}</td>
        </tr>
      </tbody>
    </v-table>
      
    </div>
  </template>
  
  <script setup>
  import axios from "axios";
  const personajes = ref([])
  onBeforeMount(() => {
    loadcharacters()
  });
  
  const  loadcharacters = async () => {
        const url = "https://gateway.marvel.com/v1/public/characters?ts=1&apikey=713c10c5e2edcc62bec72bc4676d723e&hash=e83333736a62ebe7c59b553f42434f4b"
        const { data } = await axios.get(url)
        personajes.value = data.data.results
        console.log(personajes.value)
        
    }
  
  </script>