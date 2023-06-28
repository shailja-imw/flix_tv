<script setup>
const { base_url } = useRuntimeConfig()
const route = useRoute()
const router = useRouter()
let _page = route.query._page
const { data: title, pending } = await useAsyncData('title', () =>
  $fetch(`${base_url}/title?_page=${_page}&_limit=8`)
)
const searchedShow = computed(() => {
  return title.value.filter((shows) => {
    return (
      shows.title.toLowerCase().indexOf(searchName.value.toLowerCase()) != -1
    )
  })
})
const searchName = ref('')
let shows = {
  data: searchedShow,
  isPending: pending,
}
async function clickNext() {
  _page = parseInt(_page) + 1
  refreshNuxtData('title')
  router.push(`/discover?_page=${_page}`)
  // window.location.href = `/discover?_page=${_page}`
}
async function clickPrev() {
  _page = parseInt(_page) - 1
  refreshNuxtData('title')
  router.push(`/discover?_page=${_page}`)
}
</script>

<template>
  <section class="container pt-md-5">
    <div
      class="d-flex justify-content-between card-show-brief p-3 align-items-center"
    >
      <div class="col-lg-3 col-8">
        <input
          v-model="searchName"
          class="form-control search-input"
          placeholder="Search for Movies and Tv show"
        />
      </div>
      <div>
        <NuxtLink to="/add" class="text-decoration-none white-text-link"
          >Add Show
        </NuxtLink>
      </div>
    </div>
    <div class="col-12">
      <Shows :shows="shows"></Shows>
    </div>
    <div v-if="searchedShow.length == 0">
      <NoContentFound></NoContentFound>
    </div>
    <div
      v-if="searchedShow.length != 0"
      class="d-flex justify-content-center mt-4"
    >
      <nav>
        <ul class="pagination">
          <li :class="['page-item', _page <= 1 ? 'disabled' : '']">
            <a
              class="page-link theme-pagination cursor-pointer"
              tabindex="-1"
              @click="clickPrev()"
              >Previous</a
            >
          </li>
          <li
            :class="['page-item', searchedShow.length == 0 ? 'disabled' : '']"
          >
            <button class="page-link theme-pagination" @click="clickNext()">
              Next
            </button>
          </li>
        </ul>
      </nav>
    </div>
  </section>
</template>
<style>
.theme-pagination {
  background-color: rgba(47, 128, 237, 0.1);
  color: aliceblue;
  position: relative;
  display: block;
  text-decoration: none;
  border: 1px solid rgba(47, 128, 237, 0.1);
  transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out,
    border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}

.theme-pagination:hover {
  background-color: rgba(47, 128, 237, 0.1) !important;
  color: aliceblue !important;
}

.theme-pagination:focus {
  background-color: rgba(47, 128, 237, 0.1) !important;
  color: aliceblue !important;
}

.disabled > .page-link,
.page-link.disabled {
  background-color: rgba(47, 128, 237, 0.1);
  border-color: rgba(47, 128, 237, 0.1);
}

.active > .page-link,
.page-link.active {
  background-color: #151f30;
  border-color: #151f30;
}
</style>
