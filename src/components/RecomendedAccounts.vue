<template>
  <div class="recomended-accounts">
    <ul class="recomended-accounts-list">
      <li
        class="recomended-accounts-item"
        v-for="(account, index) in recomendedAccounts"
        :key="index"
      >
        <div class="avatar-wrapper">
          <img :src="account.avatarUrl" alt="" />
        </div>
        <div class="account-info">
          <h4>{{ account.name }}</h4>
          <div class="account-info-location">
            <span class="material-icons-outlined"> location_on </span>
            <span>{{ account.location }}</span>
          </div>
        </div>
        <div class="account-action">
          <button class="add-account-btn">Add</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
  import { ref } from 'vue'
  import AnnieBatfordAvatarUrl from '../assets/images/AnnieBatford.png'
  import NancySmithAvatarUrl from '../assets/images/NancySmith.png'
  import JackBravisAvatarUrl from '../assets/images/JackBravis.png'

  const recomendedAccounts = ref([
    {
      name: 'Annie Batford',
      location: 'San Francisco',
      avatarUrl: AnnieBatfordAvatarUrl,
    },
    { name: 'Nancy Smith', location: 'London', avatarUrl: NancySmithAvatarUrl },
    {
      name: 'Jack Bravis',
      location: 'New York',
      avatarUrl: JackBravisAvatarUrl,
    },
  ])
</script>

<style lang="scss" scoped></style>
