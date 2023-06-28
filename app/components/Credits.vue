<script setup>
defineProps(['credit'])
</script>

<template>
  <div>
    <div class="img-credits">
      <img :src="credit.img_url" class="img-fluid rounded-circle" />
    </div>
    <div class="mt-3 text-center">
      <p class="">@{{ credit.name }}</p>
      <p class="mb-0 mt-0">
        Character : <span class="text-gray">{{ credit.character }}</span>
      </p>
      <p class="mb-0 mt-0">
        Role :
        <span class="text-gray">{{ useTextLowercase(credit.role) }}</span>
      </p>
    </div>
  </div>
</template>
<style>
.img-credits {
  width: 140px;
  margin: auto;
}
</style>
