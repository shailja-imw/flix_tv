<script setup>
const props = defineProps(['shows'])
const { base_url } = useRuntimeConfig()
const shows = ref(props.shows.data)
const isPending = ref(props.isPending)
const showModal = ref(false)
let id
function openModal(showId) {
  showModal.value = true
  id = showId
}
function closeModal() {
  showModal.value = false
  refreshNuxtData()
}
async function deleteShow() {
  const deleted = await useFetch(`${base_url}/title/${id}`, {
    method: 'DELETE',
  })
  window.location.href = '/discover?_page=1'
}
</script>

<template>
  <div>
    <div v-if="isPending" class="text-center mt-5">
      <div class="spinner-border text-info" role="status"></div>

      <div class="mt-3">Loading...</div>
    </div>
    <div v-else class="row">
      <div
        v-for="(show, index) in shows"
        :key="index"
        class="col-md-4 col-lg-3 col-sm-10 g-4"
      >
        <div class="card card-show-brief">
          <img
            :src="show.img_url"
            class="card-img-top img-show"
            :alt="show.title"
          />
          <div class="card-body">
            <NuxtLink :to="show.id" class="text-decoration-none white-text-link"
              ><h5 class="card-title text-truncate">
                {{ show.title }}
              </h5></NuxtLink
            >
            <div class="card-text">
              <div class="show-desc text-gray mt-2">
                {{ show.desc }}
              </div>
              <div class="d-flex justify-content-between mt-3">
                <div class="text-truncate text-gray">
                  Played: {{ show.runtime }}
                </div>
                <div class="text-truncate text-gray">{{ show.type }}</div>
                <div class="text-truncate text-gray">
                  {{ show.release_year }}
                </div>
              </div>
              <div class="d-flex justify-content-between mt-3">
                <NuxtLink :to="`/${show.id}/update`"
                  ><img
                    src="~/assets/images/icons/edit.svg"
                    class="main__table-btn btn_edit"
                /></NuxtLink>
                <img
                  src="~/assets/images/icons/delete.svg"
                  class="main__table-btn btn_delete cursor-pointer"
                  data-bs-toggle="modal"
                  data-bs-target="#deleteModal"
                  @click="openModal(show.id)"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div
    id="deleteModal"
    class="modal fade"
    tabindex="-1"
    aria-labelledby="deleteModalLabel"
    :aria-hidden="showModal ? true : false"
  >
    <div class="modal-dialog">
      <div class="modal-content modal-dark">
        <div class="modal-header">
          <h5 id="deleteModalLabel" class="modal-title">Delete Show</h5>
        </div>
        <div class="modal-body">Are you sure You want to remove the show ?</div>
        <div class="modal-footer">
          <button
            type="button"
            class="btn btn-secondary"
            data-bs-dismiss="modal"
            @click="closeModal()"
          >
            Close
          </button>
          <button
            type="button"
            class="btn btn-theme-blue"
            @click="deleteShow()"
          >
            Save changes
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<style>
.modal-dark {
  position: relative;
  display: flex;
  flex-direction: column;
  width: 100%;
  color: white;
  pointer-events: auto;
  background-color: #192842;
  background-clip: padding-box;
  outline: 0;
}

.modal-header {
  border-bottom: #151f30;
}

.modal-footer {
  border: none;
}
</style>
