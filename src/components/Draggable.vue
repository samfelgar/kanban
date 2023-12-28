<script setup lang="ts">
interface Emit {
    (e: 'dragstart', event: DragEvent, name: string): void
}

interface Props {
    name: string;
}

defineEmits<Emit>();
defineProps<Props>();
</script>

<template>
  <div
    class="bg-slate-600 w-10/12 h-32 border border-white flex items-center justify-center"
    draggable="true"
    @dragstart="$emit('dragstart', $event, name)"
  >
    {{ name }}
  </div>
</template>
