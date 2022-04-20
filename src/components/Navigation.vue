<template>
  <nav class="navigation">
    <div class="nav-links-wrapper">
      <ul
        ref="navLinks"
        class="nav-links"
        :style="`--linkHeight: ${linkHeight}px;`"
      >
        <li
          class="nav-link"
          v-for="(page, index) in pages"
          :key="index"
          :ref="skipUnwrap.itemRefs"
          :id="page.name"
          @click="handleNav(index)"
        >
          <!-- <transition> -->
          <span :class="['link-name', { active: page.active }]">{{
            page.name
          }}</span>
          <span
            :class="[
              'link-icon material-icons-outlined',
              { active: page.active },
            ]"
          >
            {{ page.icon }}
          </span>
          <!-- </transition> -->
        </li>

        <div
          ref="marker"
          class="marker"
          :style="`--marker-top-desk: ${markerTopDesk}; --marker-left-mob: ${markerLeftMob};`"
        >
          <span class="covers"></span>
        </div>
      </ul>
    </div>
  </nav>
</template>

<script setup>
  import { computed, nextTick, onBeforeUnmount, onMounted, ref } from 'vue'
  const linkHeight = ref(120)
  const marker = ref(null)
  const navLinks = ref(null)

  const markerTopDesk = computed(() => {
    const index = pages.value.indexOf(pages.value.filter((p) => p.active)[0])
    const item =
      itemRefs.value &&
      itemRefs.value.filter((item) => item.id === pages.value[index].name)[0]
    const itemY = item && item.getBoundingClientRect().y

    const yOffset = navLinks.value && navLinks.value.getBoundingClientRect().top

    return itemY - yOffset
  })

  const markerLeftMob = computed(() => {
    const index = pages.value.indexOf(pages.value.filter((p) => p.active)[0])
    const item =
      itemRefs.value &&
      itemRefs.value.filter((item) => item.id === pages.value[index].name)[0]
    const itemSize = item && item.getBoundingClientRect().width

    return index * itemSize + itemSize / 2
  })

  const showSettings = ref(false)
  const itemRefs = ref([])
  const skipUnwrap = { itemRefs }
  const pages = ref([
    {
      name: 'Profile',
      active: true,
      icon: 'person_outline',
    },
    {
      name: 'Images',
      active: false,
      icon: 'image',
    },
    {
      name: 'Files',
      active: false,
      icon: 'folder',
    },
    {
      name: 'Nube',
      active: false,
      icon: 'cloud',
    },
    {
      name: 'Settings',
      active: false,
      icon: 'settings',
    },
  ])
  const handleNav = (i) => {
    pages.value.forEach((page) => {
      page.active = false
    })
    pages.value[i].active = true
  }

  const resizeTimeout = ref(null)

  const handleResize = (e) => {
    if (resizeTimeout.value) clearTimeout(resizeTimeout.value)
    resizeTimeout.value = setTimeout(() => {
      const index = pages.value.indexOf(pages.value.filter((p) => p.active)[0])
      handleNav(index)
    }, 500)
  }
  onMounted(() => {
    window.addEventListener('resize', handleResize)
  })

  onBeforeUnmount(() => {
    window.removeEventListener('resize', handleResize)
  })
</script>

<style lang="scss" scoped></style>
