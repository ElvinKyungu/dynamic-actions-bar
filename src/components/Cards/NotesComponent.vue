<script setup lang="ts">
  import IconNotes from '../icons/IconFile.vue'
</script>
<template>
  <div class="p-4 flex flex-col items-center absolute w-full bottom-16 gap-1">
    <div class="file-result">
      <div class="flex items-center gap-3">
        <IconNotes />
        <span class="font-semibold">Changelog using GitHub</span>
      </div>
      <span class="block">
        Jun, 24
      </span>
    </div>
    <div class="file-result">
      <div class="flex items-center gap-3">
        <IconNotes />
        <span class="font-semibold">Feedback in Slack</span>
      </div>
      <span class="block">
        May, 24
      </span>
    </div>
    <div class="file-result">
      <div class="flex items-center gap-3">
        <IconNotes />
        <span class="font-semibold">Feedback in Slack</span>
      </div>
      <span class="block">
        May, 24
      </span>
    </div>
    <hr>
  </div>
</template>