<template>
  <div class="layout">
    <Sidebar ref="sidebar" />
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'

const sidebarRef = ref<HTMLElement | null>(null)

const handleKeydown = (event: KeyboardEvent) => {
  if (event.key === 'ArrowLeft') {
    sidebarRef.value?.focus()
  }
}

onMounted(() => {
  document.addEventListener('keydown', handleKeydown)
})

onBeforeUnmount(() => {
  document.removeEventListener('keydown', handleKeydown)
})
</script>

<style scoped>
.layout {
  display: flex;
}

.content {
  margin-left: 250px; /* Space for the sidebar */
  padding: 20px;
  flex: 1;
}
</style>
