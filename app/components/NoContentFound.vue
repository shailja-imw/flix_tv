<template>
  <div
    class="container mt-3 d-flex flex-column justify-content-center align-items-center"
  >
    <img
      src="~/assets/images/noContent.png"
      alt="Nocontent"
      class="img-fluid img-nocontent"
    />
    <h3>No Content Found</h3>
    <NuxtLink to="/discover?_page=1" class="text-decoration-none"
      >Discover new show</NuxtLink
    >
  </div>
</template>
<style>
.img-nocontent {
  max-height: 400px;
}
</style>
