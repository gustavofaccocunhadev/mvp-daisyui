<template>
  <div class="carousel w-full">
    <div
      v-for="(character, index) in props.characters"
      :key="index"
      :id="'slide' + index"
      class="carousel-item relative w-full"
    >
      <img :src="getImage(character)" class="w-full" />
      <div class="absolute left-5 right-5 top-1/2 flex -translate-y-1/2 transform justify-between">
        <a
          :href="'#slide' + (index === 0 ? props.characters.length - 1 : index - 1)"
          class="btn btn-circle"
          >❮</a
        >
        <a
          :href="'#slide' + (index === props.characters.length - 1 ? 0 : index + 1)"
          class="btn btn-circle"
          >❯</a
        >
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  characters: Array,
})

function getImage(url) {
  const newUrl = url.replace(
    'https://rickandmortyapi.com/api/character/',
    'https://rickandmortyapi.com/api/character/avatar/',
  )
  return `${newUrl}.jpeg`
}
</script>
