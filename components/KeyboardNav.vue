<script setup lang="ts">
  const items = ref([1, 2, 3, 4, 5, 6])
  const currentIndex = ref(0)

  const props = defineProps({
    index: {
        type: Number,
        default: 3
    },
    baseColor: String,
    selectedColor: String
  })

  const handleKeydown = (event: KeyboardEvent) => {
    switch (event.key) {
      case 'ArrowLeft':
        currentIndex.value = Math.max(0, currentIndex.value - 1)  
        break
      case 'ArrowRight':
        currentIndex.value = Math.min(items.value.length - 1, currentIndex.value + 1) 
        break
    }
  }

  onMounted(() => {
    document.addEventListener('keydown', handleKeydown)
    const elements = document.querySelectorAll<HTMLElement>('.element')
    elements.forEach(element => {
      element.addEventListener('click', (event) => event.preventDefault())
    })
  })

</script>
<template>
<div>
        Judul {{index}}<br>
        detail {{index}}<br>
        ini adalah detail {{index}}<br>

  <div
    v-for="(item, index) in items"
    :key="index"
    :class="['element', { selected: index === currentIndex }]"
    :style="{ backgroundColor: index === currentIndex ? selectedColor : baseColor }"
    tabindex="0"
  >
    {{ index + 1 }}
  </div>
</div>
</template>


<style scoped>
.element {
width: 100px;
height: 100px;
margin: 10px;
display: inline-block;
background-color: lightblue;
text-align: center;
line-height: 100px;
user-select: none;
}
.selected {
background-color: lightgreen;
}
</style>


