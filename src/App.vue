<template>
  <div class="main-container">
    <navigation />
    <div class="main-wrapper">
      <main>
        <div class="main-left">
          <search-box />
          <profile-data />
          <statistics />
          <post-now />
          <screen-play />
        </div>
        <div class="main-right">
          <top-posts />
          <linked-accounts />
        </div>
      </main>
      <aside>
        <popular />
        <recomended-accounts />
        <top-accounts />
      </aside>
    </div>
  </div>
</template>

<script setup>
  import SearchBox from './components/SearchBox.vue'
  import ProfileData from './components/ProfileData.vue'
  import Statistics from './components/Statistics.vue'
  import PostNow from './components/postNow.vue'
  import avatarUrl from './assets/images/profile-pic.png'
  import { provide } from 'vue'
  import Navigation from './components/Navigation.vue'
  import ScreenPlay from './components/ScreenPlay.vue'
  import TopPosts from './components/TopPosts.vue'
  import LinkedAccounts from './components/LinkedAccounts.vue'
  import Popular from './components/Popular.vue'
  import RecomendedAccounts from './components/RecomendedAccounts.vue'
  import TopAccounts from './components/TopAccounts.vue'

  provide('avatarUrl', avatarUrl)
</script>

<style lang="scss">
  @import './assets/css/main.scss';
</style>
