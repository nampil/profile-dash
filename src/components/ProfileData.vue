<template>
  <div class="profile-data">
    <div class="avatar">
      <img :src="avatarUrl" alt="" />
      <span class="notification-dot"></span>
    </div>
    <div>
      <p class="title-1 subtitle">Hi Sandra</p>
      <p class="title-1 title">Welcome Back!</p>
    </div>
  </div>
</template>

<script setup>
  import { inject } from 'vue'

  const avatarUrl = inject('avatarUrl')
</script>
