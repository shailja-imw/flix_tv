<script setup>
const route = useRoute()
const type = route.params.type
const { base_url } = useRuntimeConfig()
const { data: title, pending } = await useFetch(
  `${base_url}/title?type=${type}`
)

let show = {
  data: title,
  isPending: pending,
}
</script>

<template>
  <div class="container">
    <h2 class="mt-4">
      {{ type == 'SHOW' ? 'Explore All Tv Shows' : 'Explore All Movies' }}
    </h2>
    <Shows :shows="show"></Shows>
  </div>
</template>
