<script setup>

defineProps(["inicio","fin","maxLength"])
const emit = defineEmits(['next','prev']) //recojo los eventos enviados desde el componente principal App.vue
</script>


<template>
    <div class="btn-group" role="group" aria-label="Basic example">
  <button 
          @click="emit('prev')" 
          type="button"
          class="btn btn-outline-primary"
          :disabled="inicio <=0"
   > 
        Previus
  </button>
  <button 
          @click="emit('next')" 
          type="button" 
          class="btn btn-outline-primary"
          :disabled="fin >=maxLength"
   >
        Next
   </button>
</div>
</template>

