<template>
  <dialog id="modal-episode" class="modal" :class="{ 'modal-open': show }">
    <div v-if="episode" class="modal-box">
      <form method="dialog">
        <button class="btn btn-sm btn-circle btn-ghost absolute right-2 top-2" @click="closeModal">
          ✕
        </button>
      </form>
      <h3 class="text-lg font-bold py-4">
        {{ episode.name }} <BadgeEpisode>{{ episode.episode }}</BadgeEpisode>
      </h3>
      <CarrouselAvatar :characters="episode.characters" />
      <p class="py-4">
        <BadgeDate>{{ episode.air_date }}</BadgeDate>
      </p>
    </div>
    <div v-else class="modal-box">
      <div class="flex justify-center">
        <span class="loading loading-spinner loading-xl"></span>
      </div>
    </div>
  </dialog>
</template>

<script setup>
import axios from 'axios'

const props = defineProps({
  id: String,
})

const show = defineModel()
const episode = ref(null)

watch(show, (newValue) => {
  if (newValue) {
    handleGetEpisode()
  } else {
    episode.value = null
  }
})

async function handleGetEpisode() {
  try {
    const response = await axios.get(`https://rickandmortyapi.com/api/episode/${props.id}`)
    episode.value = response.data
  } catch (error) {
    console.error(error)
  }
}

function closeModal() {
  show.value = false
}
</script>
