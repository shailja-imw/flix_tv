<script setup>
definePageMeta({
  layout: 'default',
})
const { base_url: base_url } = useRuntimeConfig()
console.log(base_url)
const { data: title, pending } = await useFetch(`${base_url}/title`)
const firstFiveShow = computed(() => {
  return title?.value?.slice(0, 4)
})
let shows = {
  data: firstFiveShow,
  isPending: pending,
}
</script>
<template>
  <div>
    <section class="height-400">
      <div class="bg-video-home">
        <video
          autoplay=""
          muted=""
          playsinline=""
          src="~/assets/videos/home-bg-video.mp4"
          class="video-play"
        ></video>
      </div>
      <div class="overlay-text-bg">
        <h1>Go ahead, stream free</h1>
        <h5 class="text-gray">
          With Plex you can watch over 20,000 free movies and shows, plus Live
          TV on almost any device. What are you waiting for?
        </h5>
        <NuxtLink to="/discover?_page=1">
          <div class="btn btn-theme-blue mt-3">Discover More Shows</div>
        </NuxtLink>
      </div>
    </section>
    <section>
      <div class="container mt-4">
        <div class="d-flex justify-content-between align-items-center">
          <div><h2>Most Popular Shows</h2></div>
          <div>
            <NuxtLink
              to="/discover?_page=1"
              class="text-decoration-none white-text-link"
              >View All</NuxtLink
            >
          </div>
        </div>
        <div>
          <Shows :shows="shows"></Shows>
        </div>
      </div>
      <div class="container mt-5">
        <div class="d-flex justify-content-between align-items-center">
          <div><h2>Tv Shows</h2></div>
          <div>
            <NuxtLink
              to="/discover/SHOW"
              class="text-decoration-none white-text-link"
              >View All</NuxtLink
            >
          </div>
        </div>
        <div>
          <Shows :shows="shows"></Shows>
        </div>
      </div>
      <div class="container mt-5">
        <div class="d-flex justify-content-between align-items-center">
          <div><h2>Movies</h2></div>
          <div>
            <NuxtLink
              to="/discover/MOVIE"
              class="text-decoration-none white-text-link"
              >View All</NuxtLink
            >
          </div>
        </div>
        <div>
          <Shows :shows="shows"></Shows>
        </div>
      </div>
    </section>
  </div>
</template>
<style>
.bg-video-home {
  right: 0;
  left: unset;
  position: absolute;
  -webkit-mask-image: url(data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9Im5vIj8+PCFET0NUWVBFIHN2ZyBQVUJMSUMgIi0vL1czQy8vRFREIFNWRyAxLjEvL0VOIiAiaHR0cDovL3d3dy53My5vcmcvR3JhcGhpY3MvU1ZHLzEuMS9EVEQvc3ZnMTEuZHRkIj48c3ZnIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHZpZXdCb3g9IjAgMCAxOTIwIDEwODAiIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSIgeG1sbnM6c2VyaWY9Imh0dHA6Ly93d3cuc2VyaWYuY29tLyIgc3R5bGU9ImZpbGwtcnVsZTpldmVub2RkO2NsaXAtcnVsZTpldmVub2RkO3N0cm9rZS1saW5lam9pbjpyb3VuZDtzdHJva2UtbWl0ZXJsaW1pdDoyOyI+PGcgdHJhbnNmb3JtPSJtYXRyaXgoMS44ODIwNSwwLDAsMS43MDg2MywtNDQ4LjgzNSwxMjIuOTgyKSI+PGcgc3R5bGU9ImZpbHRlcjp1cmwoI19FZmZlY3QxKTsiPjxwYXRoIGQ9Ik0xMjg2LjgxLDEyMy42NTdDMTI4Ni44MSw1Ny4yMDIgMTIzNy44MywzLjI0OCAxMTc3LjQ5LDMuMjQ4TDYyMi40MjIsMy4yNDhDNTYyLjA5LDMuMjQ4IDUxMy4xMDgsNTcuMjAyIDUxMy4xMDgsMTIzLjY1N0w1MTMuMTA4LDM2NC40NzRDNTEzLjEwOCw0MzAuOTMgNTYyLjA5LDQ4NC44ODMgNjIyLjQyMiw0ODQuODgzTDExNzcuNDksNDg0Ljg4M0MxMjM3LjgzLDQ4NC44ODMgMTI4Ni44MSw0MzAuOTMgMTI4Ni44MSwzNjQuNDc0TDEyODYuODEsMTIzLjY1N1oiIHN0eWxlPSJmaWxsOiNmZmY7Ii8+PC9nPjwvZz48ZGVmcz48ZmlsdGVyIGlkPSJfRWZmZWN0MSIgZmlsdGVyVW5pdHM9InVzZXJTcGFjZU9uVXNlIiB4PSItMTI0LjQ5NCIgeT0iLTY5OS4wNjgiIHdpZHRoPSIyMDQ4LjkiIGhlaWdodD0iMTg4Ni4yNyI+PGZlR2F1c3NpYW5CbHVyIGluPSJTb3VyY2VHcmFwaGljIiBzdGREZXZpYXRpb249IjExMS4yNyIvPjwvZmlsdGVyPjwvZGVmcz48L3N2Zz4=);
  mask-image: url(data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiIHN0YW5kYWxvbmU9Im5vIj8+PCFET0NUWVBFIHN2ZyBQVUJMSUMgIi0vL1czQy8vRFREIFNWRyAxLjEvL0VOIiAiaHR0cDovL3d3dy53My5vcmcvR3JhcGhpY3MvU1ZHLzEuMS9EVEQvc3ZnMTEuZHRkIj48c3ZnIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHZpZXdCb3g9IjAgMCAxOTIwIDEwODAiIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSIgeG1sbnM6c2VyaWY9Imh0dHA6Ly93d3cuc2VyaWYuY29tLyIgc3R5bGU9ImZpbGwtcnVsZTpldmVub2RkO2NsaXAtcnVsZTpldmVub2RkO3N0cm9rZS1saW5lam9pbjpyb3VuZDtzdHJva2UtbWl0ZXJsaW1pdDoyOyI+PGcgdHJhbnNmb3JtPSJtYXRyaXgoMS44ODIwNSwwLDAsMS43MDg2MywtNDQ4LjgzNSwxMjIuOTgyKSI+PGcgc3R5bGU9ImZpbHRlcjp1cmwoI19FZmZlY3QxKTsiPjxwYXRoIGQ9Ik0xMjg2LjgxLDEyMy42NTdDMTI4Ni44MSw1Ny4yMDIgMTIzNy44MywzLjI0OCAxMTc3LjQ5LDMuMjQ4TDYyMi40MjIsMy4yNDhDNTYyLjA5LDMuMjQ4IDUxMy4xMDgsNTcuMjAyIDUxMy4xMDgsMTIzLjY1N0w1MTMuMTA4LDM2NC40NzRDNTEzLjEwOCw0MzAuOTMgNTYyLjA5LDQ4NC44ODMgNjIyLjQyMiw0ODQuODgzTDExNzcuNDksNDg0Ljg4M0MxMjM3LjgzLDQ4NC44ODMgMTI4Ni44MSw0MzAuOTMgMTI4Ni44MSwzNjQuNDc0TDEyODYuODEsMTIzLjY1N1oiIHN0eWxlPSJmaWxsOiNmZmY7Ii8+PC9nPjwvZz48ZGVmcz48ZmlsdGVyIGlkPSJfRWZmZWN0MSIgZmlsdGVyVW5pdHM9InVzZXJTcGFjZU9uVXNlIiB4PSItMTI0LjQ5NCIgeT0iLTY5OS4wNjgiIHdpZHRoPSIyMDQ4LjkiIGhlaWdodD0iMTg4Ni4yNyI+PGZlR2F1c3NpYW5CbHVyIGluPSJTb3VyY2VHcmFwaGljIiBzdGREZXZpYXRpb249IjExMS4yNyIvPjwvZmlsdGVyPjwvZGVmcz48L3N2Zz4=);
  -webkit-mask-position: left bottom;
  mask-position: left bottom;
  -webkit-mask-size: 100%;
  mask-size: 100%;
  height: 480px;
  width: calc(calc(100vw / 2.5) * 1.8);
}

.height-400 {
  height: 500px;
}
.video-play {
  position: relative;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.overlay-text-bg {
  width: 50%;
  max-width: 100%;
  text-align: left;
  display: flex;
  flex-wrap: nowrap;
  flex-flow: column;
  position: relative;
  padding-top: 8%;
  padding-left: 16%;
}

@media screen and (max-width: 767px) {
  .video-play {
    visibility: hidden;
  }

  .overlay-text-bg {
    width: 100%;
    padding: 40% 10px;
  }
}
</style>
