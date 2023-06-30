<script setup>
const { base_url } = useRuntimeConfig()
const route = useRoute()
const { data: show } = await useFetch(`${base_url}/title/${route.params.id}`)
</script>

<template>
  <div class="container mt-md-3">
    <div class="row pt-md-5">
      <div class="col-md-3">
        <img :src="show.img_url" class="img-fluid img-details" />
      </div>
      <div class="col-md-9">
        <h3 class="pt-2">{{ show.title }}</h3>
        <div class="pt-2 text-gray">{{ show.desc }}</div>
        <div class="pt-2">
          Type :
          <span class="text-gray"> {{ useTextLowercase(show.type) }}</span>
        </div>
        <div class="pt-2">
          Run Time : <span class="text-gray"> {{ show.runtime }}</span>
        </div>
        <div class="pt-2">
          Release Year :
          <span class="text-gray"> {{ show.release_year }}</span>
        </div>
        <div v-if="show.genres" class="mt-2">
          Genres :
          <span class="pe-3 text-gray"> {{ show.genres }}</span>
        </div>
        <div v-if="show.production_countries" class="mt-2">
          Production Country :
          <span class="pe-3 text-gray"> {{ show.production_countries }}</span>
        </div>
        <div class="mt-3 d-flex align-items-center">
          <div class="d-flex align-items-center">
            <div>
              <font-awesome-icon
                icon="fa-solid fa-star"
                class="text-theme-blue icon-height pe-2"
              />
            </div>
            <div class="text-theme-blue">
              <span class="text-theme-blue h4">8.0</span>
              <div class="text-gray">{{ show.runtime }} votes</div>
            </div>
          </div>
          <div class="ms-3 d-flex align-items-center">
            <div>
              <font-awesome-icon
                icon="fas fa-heart"
                class="text-danger icon-height mx-2"
              />
            </div>
            <div class="text-gray">
              {{ useTextLowercase(show.type) }}
            </div>
          </div>
        </div>
      </div>
    </div>
    <div v-if="show.credits.length > 0" class="pt-5">
      <h3>Credits</h3>
      <div class="mt-4 row">
        <div
          v-for="(credit, index) of show.credits"
          :key="index"
          class="col-lg-2 col-md-3 col-6 g-3"
        >
          <Credits :credit="credit"></Credits>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.img-details {
  height: 380px;
  width: 300px;
}

@media (max-width: 767px) {
  .img-details {
    height: auto;
    width: auto;
  }
}

.icon-height {
  height: 38px;
}
</style>
