<template>
  <div class="top-accounts">
    <h3>Top Accounts</h3>
    <ul class="top-accounts-list">
      <li v-for="(acc, i) in topAccounts" :key="i">
        <div class="top-account-item">
          <div
            class="img-bg"
            :style="`background-image: url(${acc.imgUrl})`"
          ></div>
          <img v-if="acc.royalty" class="icon" :src="crownIconUrl" alt="" />
          <h4>
            <a href="#">{{ acc.name }}</a>
          </h4>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
  import { ref } from 'vue'
  import Mark from '../assets/images/mark.png'
  import Max from '../assets/images/max.png'
  import Samantha from '../assets/images/samantha.png'
  import crownIconUrl from '../assets/icons/crown.svg'

  const topAccounts = ref([
    { name: 'Mark Damon', royalty: true, imgUrl: Mark },
    { name: 'Max Khudoyan', royalty: false, imgUrl: Max },
    { name: 'Samantha Liu', royalty: false, imgUrl: Samantha },
  ])
</script>

<style lang="scss" scoped></style>
