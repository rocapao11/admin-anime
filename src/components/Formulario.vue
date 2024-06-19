<template>
  <div class="md:w-1/2">
    <h2 class="font-black text-3xl text-center">Seguimiento Anime</h2>

    <p class="text-lg mt-5 text-center mb-10">
      Añade Animes y
      <span class="text-indigo-600 font-bold">Adminístralos</span>
    </p>
    <Alerta
      v-if="alerta.mensaje"
      :alerta="alerta"
    />
    <form
      class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
      @submit.prevent="validar"
    >
      <div class="mb-5">

        <label 
          for="anime"
          class="block text-gray-700 uppercase font-bold"
        >
          Nombre anime
        </label>
        <input
          id="anime"
          type="text"
          placeholder="Nombre del anime"
          class="border-2 w-full p-2 mt-2 placeholder-gray-400 ronded-md"
          :value="nombre"
          @input="$emit('update:nombre', $event.target.value)"
          />
      </div>

      <div class="mb-5">
        <label 
          for="episodios"
          class="block text-gray-700 uppercase font-bold"
        >
          Episodios vistos
        </label>
        <input
          id="episodios"
          type="text"
          placeholder="Episodios del anime completados"
          class="border-2 w-full p-2 mt-2 placeholder-gray-400 ronded-md"
          :value="episodio"
          @input="$emit('update:episodio', $event.target.value)"
          />
      </div>
      <div class="mb-5">
        <label 
          for="status"
          class="block text-gray-700 uppercase font-bold"
        >
          Estatus
        </label>
        <input
          id="status"
          type="text"
          placeholder="Completo / Por ver / En espera"
          class="border-2 w-full p-2 mt-2 placeholder-gray-400 ronded-md"
          :value="status"
          @input="$emit('update:status', $event.target.value)"/>
      </div>

    <!-- </div>
      <div class="mb-5">
        <label 
          for="status"
          class="block text-gray-700 uppercase font-bold"
        >
          Estatus
        </label>
        <input
          id="status"
          type="text"
          placeholder="Completo / Por ver / En espera"
          class="border-2 w-full p-2 mt-2 placeholder-gray-400 ronded-md"
          :value="status"
          @input="$emit('update:status', $event.target.value)"/>
      </div>

      <div class="card">
        <AutoComplete v-model="value" dropdown :suggestions="items" @complete="search" />
        </div> -->

      <div class="mb-5">
        <label 
          for="inicio"
          class="block text-gray-700 uppercase font-bold"
        >
          Fecha de inicio
        </label>
        <input
          id="inicio"
          type="date"
          placeholder="Espectador del anime"
          class="border-2 w-full p-2 mt-2 placeholder-gray-400 ronded-md"
          :value="start"
          @input="$emit('update:start', $event.target.value)"
          />
      </div>
      <div class="mb-5">
        <label 
          for="end"
          class="block text-gray-700 uppercase font-bold"
        >
          Fecha de fin
        </label>
        <input
          id="end"
          type="date"
          placeholder="Espectador del anime"
          class="border-2 w-full p-2 mt-2 placeholder-gray-400 ronded-md"
          :value="end"
          @input="$emit('update:end', $event.target.value)"/>
      </div>
      <div class="mb-5">
        <label 
          for="comentario"
          class="block text-gray-700 uppercase font-bold"
        >
          Comentarios
        </label>
        <textarea
          id="comentario"
          placeholder="Comentarios del anime"
          class="border-2 w-full p-2 mt-2 placeholder-gray-400 ronded-md h-40"
          :value="coments"
          @input="$emit('update:coments', $event.target.value)"
        />
      </div>
      <input
        type="submit"
        class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
        :value="[editando ? 'Guardar Cambios' : 'Registrar Anime']"
        />
    </form>
  </div>
</template>

<script setup>
  import { ref, reactive, computed } from 'vue'
  import Alerta from './Alerta.vue'

  const alerta = reactive({
    tipo: '',
    mensaje: ''
  })

  const emit = defineEmits(['update:nombre', 'update:episodio', 'update:status', 'update:start', 'update:end', 'update:coments', 'guardar-anime'])

  const props = defineProps({
    id: {
      type:[String, null],
      required:true
    },    
    nombre: {
      type: String,
      required: true
    },
    episodio: {
      type: String,
      required: true
    },
    status: {
      type: String,
      required: true
    },
    start: {
      type: String,
      required: true
    },
    end: {
      type: String,
      required: true
    },
    coments: {
      type: String,
      required: true
    },
  })

//   const value = ref("");
//     const items = ref([]);

//     const search = (event) => {
//     let _items = [...Array(10).keys()];

//     items.value = event.query ? [...Array(10).keys()].map((item) => event.query + '-' + item) : _items;
// }

  const validar = () => {
    if(Object.values(props).includes('')) {
      alerta.mensaje = 'Todos los campos son obligatorios'
      alerta.tipo= 'error'
      return
    }
    emit('guardar-anime')
    alerta.mensaje = 'Anime Almacenado Correctamente'
    alerta.tipo= 'exito'
    setTimeout(() => {
      Object.assign(alerta,{
        tipo: '',
        mensaje: ''
      })
    }, 3000)
  }

  const editando = computed(() => {
    return props.id
  })

  

</script>
