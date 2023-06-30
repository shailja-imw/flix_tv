<script setup>
const { base_url } = useRuntimeConfig()
const router = useRouter()
const route = useRoute()
const id = route.params.id
const noDataFound = ref(false)
let show = {}
const { data } = await useFetch(`${base_url}/title/${id}`)
if (data.value === null) {
  noDataFound.value = true
} else {
  noDataFound.value = false
  show = data
}
async function apiCall(showDetails) {
  const data = await useFetch(`${base_url}/title/${id}`, {
    headers: { 'Content-type': 'application/json' },
    method: 'PUT',
    body: showDetails.id ? JSON.stringify(showDetails) : '',
  })
  return data
}
async function handleSubmit(showDetails) {
  const data = await apiCall(showDetails)
  if (data.error.value == null) {
    alert('Show updated Successfully')
    refreshNuxtData('showDeatils')
    router.push('/discover?_page=1')
  } else {
    alert(data.error.value)
  }
}
</script>

<template>
  <div class="container">
    <div v-if="noDataFound">
      <NoContentFound></NoContentFound>
    </div>
    <div v-else>
      <h3 class="text-center mt-4 mb-3">Update Show</h3>
      <Upsert :shows="show" @handle-submit="handleSubmit"></Upsert>
    </div>
  </div>
</template>
