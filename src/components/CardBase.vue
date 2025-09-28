<template>
  <div
    @click="emit('onClickEpisode')"
    class="card bg-base-100 shadow-sm hover:bg-neutral-content hover:shadow-md cursor-pointer"
  >
    <div class="avatar-group -space-x-6 m-4">
      <div class="avatar" v-for="character in charactersFilter">
        <div class="w-12">
          <img :src="getImage(character)" />
        </div>
      </div>
      <div v-if="countCharacters > 0" class="avatar avatar-placeholder">
        <div class="bg-neutral text-neutral-content w-12">
          <span>+{{ countCharacters }}</span>
        </div>
      </div>
    </div>

    <div class="card-body">
      <h2 class="card-title">
        {{ name }}
        <BadgeEpisode>{{ episode }}</BadgeEpisode>
      </h2>
      <div class="card-actions justify-start">
        <BadgeDate>{{ airDate }}</BadgeDate>
      </div>
    </div>
  </div>
</template>

<script setup>
const emit = defineEmits(['onClickEpisode'])

const props = defineProps({
  name: String,
  episode: String,
  airDate: String,
  characters: Array,
})

const charactersFilter = computed(() => {
  if (props.characters.length > 5) {
    return props.characters.splice(0, 5)
  } else {
    return 0
  }
})

const countCharacters = computed(() => {
  if (props.characters.length > 5) return props.characters.length - 5
  else return props.characters.length
})

function getImage(url) {
  const newUrl = url.replace(
    'https://rickandmortyapi.com/api/character/',
    'https://rickandmortyapi.com/api/character/avatar/',
  )
  return `${newUrl}.jpeg`
}
</script>
