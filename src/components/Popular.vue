<template>
  <div class="popular-wrapper">
    <div
      class="popular"
      :style="`background-image: url(${popularAccountImgUrl})`"
    >
      <h3 class="title">Popular this week</h3>
      <div class="spacer"></div>
      <div class="account-info">
        <img class="icon" :src="crownIconUrl" alt="" />
        <h4 class="account-name"><a href="#">Jen Smith</a></h4>
        <div class="rating">
          <span class="material-icons-outlined"> star </span>
          <span class="material-icons-outlined"> star </span>
          <span class="material-icons-outlined"> star </span>
          <span class="material-icons-outlined"> star </span>
          <span class="material-icons-outlined"> star_outline </span>
        </div>
        <p class="review-count">230.547</p>
      </div>
    </div>
  </div>
</template>

<script setup>
  import popularAccountImgUrl from '../assets/images/popular-accout.png'
  import crownIconUrl from '../assets/icons/crown.svg'
</script>

<style lang="scss" scoped></style>
