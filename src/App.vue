<template>
  <div class="container mx-auto mt-20">
    <Header />

    <div class="mt-12 md:flex">
      <formulario
        v-model:nombre="anime.nombre"
        v-model:episodio="anime.episodio"
        v-model:status="anime.status"
        v-model:start="anime.start"
        v-model:end="anime.end"
        v-model:coments="anime.coments"
        @guardar-anime="guardarAnime "
        :id="anime.id"
      />

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administra tus animes</h3>
        
        <div v-if="animes.length > 0">

          <p class="text-lg mt-5 text-center mb-10">
            Información de 
            <span class="text-indigo-600 font-bold">Animes</span>
          </p>

          <Anime 
            v-for="anime in animes"
            :anime="anime"
            @actualizar-anime = "actualizarAnime"
            @eliminar-anime="eliminarAnime"
          />
        </div>
        <p v-else class="mt-10 text-2xl text-center">No hay Animes en la lista</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted, watch } from 'vue'
import { uid } from 'uid'
import Header from './components/Header.vue'
import Formulario from './components/Formulario.vue' 
import Anime from './components/Anime.vue'

  const animes = ref([])


  const anime = reactive({
    id: null,
    nombre: '',
    episodio: '',
    status: '',
    start:'',
    end:'',
    coments:'',
  })

  watch( animes, () => {
    guardarLocalStorage();
  }, {
    deep:true
  })

  const guardarLocalStorage = () => {
    localStorage.setItem('animes', JSON.stringify(animes.value))
  }

  onMounted(() => {
    const animesStorage = localStorage.getItem('animes')
    if(animesStorage){
      animes.value = JSON.parse(animesStorage)
    }
  })

  const guardarAnime = () =>{
    if(anime.id){
      const { id } = anime
      const i = animes.value.findIndex(anime => anime.id === id )
      animes.value[i] = {...anime}
    } else {
      animes.value.push({
      ...anime,
      id:uid()
      })
    }


    Object.assign(anime,{
      nombre: '',
      episodio: '',
      status: '',
      start: '',
      end: '',
      coments:'',
      id: null,
    })
  }

  const actualizarAnime = (id) => {
    const animeEditar = animes.value.filter( anime => anime.id === id)[0]
    Object.assign(anime, animeEditar)
  }

  const eliminarAnime = (id) => {
    animes.value = animes.value.filter( anime => anime.id !== id)
  }
</script>
