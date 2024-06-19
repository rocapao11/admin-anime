<template>
  <div class="mx-5 my-10 bg-white shadow-md px-5 py-10 rounded-xl">
    <p class="font-bold mb-3 text-gray-700 uppercase">ID:
      <span class="font-normal normal-case">
        {{ anime.id }}
      </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">Nombre:
      <span class="font-normal normal-case">
        {{ anime.nombre }}
      </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">Episodios: 
      <span class="font-normal normal-case">
        {{ anime.episodio }}
      </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">Estatus: 
      <span class="font-normal normal-case">
        {{ anime.status }}
      </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">Fecha inicio:
      <span class="font-normal normal-case">
        {{ anime.start }}
      </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">Fecha fin:
      <span class="font-normal normal-case">
        {{ anime.end }}
      </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">Comentarios:
      <span class="font-normal normal-case">
        {{ anime.coments }}
      </span>
    </p>

    <div class="grid md:grid-cols-2  gap-5 mt-10 ">
      <button 
        type="button"
        class="block w-full py-2 px-10 bg-indigo-600 hover:bg-indigo-700 text-white font-bold uppercase rounded-lg"
        @click = "$emit('actualizar-anime', anime.id)"
      >Editar</button>

      <button 
        type="button"
        class="block w-full py-2 px-10 bg-red-600 hover:bg-red-700 text-white font-bold uppercase rounded-lg"
        @click = "$emit('eliminar-anime', anime.id)"
        >Eliminar</button>
    </div>
  </div>
</template>

<script setup>
defineEmits(['actualizar-anime', 'eliminar-anime'])

  defineProps({
    anime: {
      type:Object,
      required: true
    }
  })
</script>
