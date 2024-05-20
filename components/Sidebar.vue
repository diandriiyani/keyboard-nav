<template>
  <aside ref="sidebar" class="sidebar" tabindex="0">
    <ul>
      <li v-for="(link, index) in links" :key="index">
        <nuxt-link
          ref="link"
          :to="link.path"
          tabindex="-1"
          :class="['no-click', { 'is-focused': currentIndex === index }]"
        >
          {{ link.name }}
        </nuxt-link>
      </li>
    </ul>
  </aside>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const sidebar = ref<HTMLElement | null>(null)
const links = ref([
  { name: 'Home', path: '/' },
  { name: 'About', path: '/' },
])

const currentIndex = ref(0)

const handleKeydown = (event: KeyboardEvent) => {
  const linkRefs = sidebar.value?.querySelectorAll('a')
  if (!linkRefs) return

  if (event.key === 'ArrowDown') {
    event.preventDefault()
    if (currentIndex.value < linkRefs.length - 1) {
      currentIndex.value++
      ;(linkRefs[currentIndex.value] as HTMLElement).focus()
    }
  } else if (event.key === 'ArrowUp') {
    event.preventDefault()
    if (currentIndex.value > 0) {
      currentIndex.value--
      ;(linkRefs[currentIndex.value] as HTMLElement).focus()
    }
  }
}

onMounted(() => {
  sidebar.value?.focus() // Focus the sidebar initially
  const linkRefs = sidebar.value?.querySelectorAll('a')
  if (linkRefs && linkRefs.length > 0) {
    (linkRefs[0] as HTMLElement).focus() // Focus the first link
  }

  document.addEventListener('keydown', handleKeydown)
})
</script>


<style scoped>
.sidebar {
  width: 250px;
  height: 100%;
  background-color: #f0f0f0;
  padding: 20px;
  position: fixed;
  left: 0;
  top: 0;
  bottom: 0;
  outline: none; /* Remove outline when sidebar is focused */
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 10px 0;
}

a {
  text-decoration: none;
  color: inherit;
  pointer-events: none; /* Disable mouse clicks */
}

a:focus,
a.is-focused {
  background-color: #ddd; /* Highlight focused link */
}
</style>

