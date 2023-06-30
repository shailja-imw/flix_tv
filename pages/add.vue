<script setup>
const { base_url: baseUrl } = useRuntimeConfig()
const router = useRouter()
let show = {
  id: 's_' + Math.random(),
  title: '',
  desc: '',
  type: '',
  release_year: '',
  run_time: '',
  genres: '',
  img_url: '',
  production_country: '',
  credits: [
    {
      person_id: Math.random(),
      title_id: '',
      name: '',
      character: '',
      role: '',
      img_url: '',
    },
  ],
}

async function apiCall(showDetails) {
  const data = await useFetch(`${baseUrl}/title`, {
    headers: { 'Content-type': 'application/json' },
    method: 'POST',
    body: JSON.stringify(showDetails),
  })
  return data
}
async function handleSubmit(showDetails) {
  const data = await apiCall(showDetails)
  if (data.error.value == null) {
    alert('Show added successfully')
    refreshNuxtData('showDeatils')
    router.push('/discover?_page=1')
  } else {
    alert(data.error.value)
  }
}
</script>

<template>
  <div class="container">
    <h3 class="text-center my-2">Add New Shows</h3>
    <Upsert :shows="show" @handle-submit="handleSubmit"></Upsert>
  </div>
</template>
