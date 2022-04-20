<template>
  <div class="top-posts">
    <h3>Top Posts</h3>
    <div class="posts-container">
      <div v-for="(post, i) in posts" :key="i" class="post-item">
        <div
          class="img-bg"
          :style="`background-image: url(${post.imgUrl});`"
        ></div>
        <span class="pots-title">{{ post.title }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
  import SynergyImgUrl from '../assets/images/synergy.png'
  import UrbanImgUrl from '../assets/images/urban.png'
  import GardensImgUrl from '../assets/images/garden.png'
  import TravelImgUrl from '../assets/images/travel.png'

  const posts = [
    { title: 'Synergy', imgUrl: SynergyImgUrl },
    { title: 'Urban', imgUrl: UrbanImgUrl },
    { title: 'Gardens', imgUrl: GardensImgUrl },
    { title: 'Travel', imgUrl: TravelImgUrl },
  ]
</script>

<style lang="scss" scoped></style>
