<template>
  <SidebarLayouts>
    <div>
      <div v-for="(item, index) in items" :key="index">
        <KeyboardNav v-if="currentIndex === index" :index="index+1" :baseColor="item.color" :selectedColor="item.selected" />
      </div>
    </div>
  </SidebarLayouts>
  </template>
  
  <script setup lang="ts">
  const items= [
        {
            color: 'lightblue',
            selected: 'lightgreen'
        },
        {
            color: 'blue',
            selected: 'green'
        },
        {
            color: 'lightyellow',
            selected: 'lightpink'
        },
        {
            color: 'yellow',
            selected: 'pink'
        }
    ]
  const currentIndex = ref(0)
  
  function handleArrowUp() {
    if (currentIndex.value > 0) {
      currentIndex.value--
    }
  }
  
  function handleArrowDown() {
    if (currentIndex.value < items.length - 1) {
      currentIndex.value++
    }
  }
  
  onMounted(() => {
    document.addEventListener('keydown', (event) => {
      if (event.key === 'ArrowUp') {
        handleArrowUp()
      } else if (event.key === 'ArrowDown') {
        handleArrowDown()
      }
    })
  })
  </script>
  