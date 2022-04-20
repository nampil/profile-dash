<template>
  <div class="post-now">
    <div class="avatar-wrapper">
      <img :src="avatarUrl" alt="" />
    </div>
    <div class="post-form">
      <div class="input-group">
        <input name="post-title" id="post-title" type="text" placeholder=" " />
        <label for="post-title">My lates trip was...</label>
      </div>
      <div class="post-props">
        <div class="post-visibility">
          <span class="material-icons-outlined"> lock </span>
          <span>Post Private</span>
        </div>
        <div class="post-category">
          <div class="post-category-group">
            <span class="post-category-lbl">Post to</span>
            <button
              class="post-category-btn"
              @click="showCatOptions = !showCatOptions"
            >
              <span class="btn-text">{{ catSelected }}</span>
              <span class="material-icons-outlined"> arrow_drop_down </span>
              <ul :class="['category-select', { showCatOptions }]">
                <li
                  v-for="(cat, index) in catOptions"
                  :key="index"
                  @click="catSelected = catOptions[index]"
                >
                  {{ cat.charAt(0).toUpperCase() + cat.substring(1) }}
                </li>
              </ul>
            </button>
          </div>
        </div>
      </div>
    </div>
    <button class="post-now-btn"><span>Post Now</span></button>
  </div>
</template>

<script setup>
  import { inject, ref } from 'vue'
  const avatarUrl = inject('avatarUrl')
  const catOptions = ['travel', 'personal', 'marketing']
  const catSelected = ref('travel')
  const showCatOptions = ref(false)
</script>

<style lang="scss" scoped></style>
