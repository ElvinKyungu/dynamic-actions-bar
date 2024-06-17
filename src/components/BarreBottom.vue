<template>
  <nav class="container flex flex-col relative w-[25rem]">
    <ul class="flex text-red-800 gap-6 justify-center z-20 items-center bg-[#e2ba97] rounded-lg">
      <li 
        class="
          flex items-center hover:bg-black hover:text-white 
          delay-100 p-3 cursor-pointer rounded-lg gap-3 transition-colors 
        "
        @mouseenter="handleMouseEnter(0)"
        @mouseleave="handleMouseLeave"
      >
        <IconCalendar />
        <span>Apps</span>
      </li>
      <li 
        class="
          flex items-center hover:bg-black hover:text-white 
          delay-100 p-3 cursor-pointer rounded-lg gap-3 transition-colors
        " 
        @mouseenter="handleMouseEnter(1)"
        @mouseleave="handleMouseLeave"
      >
        <IconCode />
        <span>Components</span>
      </li>
      <li 
        class="
          flex items-center hover:bg-black hover:text-white 
          delay-100 p-3 cursor-pointer rounded-lg gap-3 transition-colors
        " 
        @mouseenter="handleMouseEnter(2)"
        @mouseleave="handleMouseLeave"
      >
        <IconFile />
        <span>Notes</span>
      </li>
    </ul>
    <div 
      ref="container" 
      class="
        absolute bg-[#e2ba97] backdrop-blur-xl bottom-0 left-1/2 -translate-x-1/2
        overflow-hidden rounded-2xl container p-4
      "
    >
      <div v-show="activeComponent === 0" ref="details0">
        <AppCard />
      </div>
      <div v-show="activeComponent === 1" ref="details1">
        <ComponentCard />
      </div>
      <div v-show="activeComponent === 2" ref="details2">
        <NotesComponent />
      </div>
    </div>
  </nav>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import gsap from 'gsap'
import IconCode from '@/components/icons/IconCode.vue'
import IconFile from '@/components/icons/IconFile.vue'
import IconCalendar from '@/components/icons/IconCalendar.vue'
import AppCard from './Cards/AppCard.vue'
import ComponentCard from './Cards/ComponentCard.vue'
import NotesComponent from './Cards/NotesComponent.vue'

const activeComponent = ref<number | null>(null)
const container = ref(null)
const details0 = ref(null)
const details1 = ref(null)
const details2 = ref(null)

const duration = 0.75
const duration2 = 0.3
const ease = 'elastic.out(1, 0.5)'

const handleMouseEnter = (index: number) => {
  activeComponent.value = index
  gsap.to(container.value, {
    width: [500, 460, 480][index],
    height: [222, 194, 136][index] + 100,
    y: 17,
    borderRadius: 24,
    duration: duration,
    ease: ease,
  })
  gsap.to(details0.value, { 
    opacity: index === 0 ? 1 : 0, 
    duration: duration2, 
    zIndex: index === 0 ? 2 : 1 
  })
  gsap.to(details1.value, { 
    opacity: index === 1 ? 1 : 0, 
    duration: duration2, 
    zIndex: index === 1 ? 2 : 1 
  })
  gsap.to(details2.value, { 
    opacity: index === 2 ? 1 : 0, 
    duration: duration2, 
    zIndex: index === 2 ? 2 : 1 
  })
}

const handleMouseLeave = () => {
  console.log("hey");
  
  const isHoveringDetails = [details0.value, details1.value, details2.value]
    .some(detail => detail?.matches(':hover'))
  if (isHoveringDetails) return
  mouseleaveDetails()
}

const mouseleaveDetails = () => {
  gsap.to(container.value, {
    width: 410,
    height: 48,
    y: 0,
    borderRadius: 16,
    duration: duration,
    ease: ease,
  })
  gsap.to(details0.value, { opacity: 0, duration: 0, zIndex: 1 })
  gsap.to(details1.value, { opacity: 0, duration: 0, zIndex: 1 })
  gsap.to(details2.value, { opacity: 0, duration: 0, zIndex: 1 })
  activeComponent.value = null
}

onMounted(() => {
  details0.value.addEventListener('mouseleave', handleMouseLeave)
  details1.value.addEventListener('mouseleave', handleMouseLeave)
  details2.value.addEventListener('mouseleave', handleMouseLeave)
})
</script>

<style scoped>

</style>
