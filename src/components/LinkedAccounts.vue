<template>
  <div class="linked-accounts">
    <h3>Linked Accounts</h3>
    <div class="accounts-links">
      <div class="account-link" v-for="(account, i) in accounts" :key="i">
        <a href="#" rel="noopener noreferrer">
          <component :is="account.icon"></component>
        </a>
      </div>
    </div>
  </div>
</template>

<script setup>
  import Dropbox from '../assets/icons/Dropbox.vue'
  import Vimeo from '../assets/icons/Vimeo.vue'
  import Twitter from '../assets/icons/Twitter.vue'
  const accounts = [
    { title: 'Dropbox', icon: Dropbox },
    { title: 'Vimeo', icon: Vimeo },
    { title: 'Twitter', icon: Twitter },
  ]
</script>

<style lang="scss" scoped></style>
