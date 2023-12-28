<script setup lang="ts">
import { ref } from "vue";
import Draggable from "./components/Draggable.vue";

const tasks = ref<string[]>([]);

const handleOnDrag = (event: DragEvent, name: string) => {
  event.dataTransfer?.setData("name", name);
};

const handleOnDrop = (event: DragEvent) => {
  const data = event.dataTransfer?.getData("name");

  if (typeof data === "undefined") {
    return;
  }

  tasks.value = tasks.value.filter((task) => task !== data);
  tasks.value.push(data);
};
</script>

<template>
  <div>
    <h1 class="text-3xl my-10 ml-10">Kanban</h1>
    <div class="flex gap-4 mx-5">
      <div
        class="flex flex-col justify-center items-center gap-2 w-1/2 py-4 border-4 text-white text-center"
      >
        <Draggable name="Task 1" @dragstart="handleOnDrag" />
        <Draggable name="Task 2" @dragstart="handleOnDrag" />
        <Draggable name="Task 3" @dragstart="handleOnDrag" />
        <Draggable name="Task 4" @dragstart="handleOnDrag" />
        <Draggable name="Task 5" @dragstart="handleOnDrag" />
      </div>
      <div
        class="flex flex-col justify-center items-center gap-2 py-4 text-white text-center w-1/2 border-4"
        @dragover.prevent
        @drop="handleOnDrop"
      >
        <Draggable
          v-for="task of tasks"
          :key="task"
          :name="task"
          @dragstart="handleOnDrag"
        />
      </div>
    </div>
  </div>
</template>

<style scoped></style>
