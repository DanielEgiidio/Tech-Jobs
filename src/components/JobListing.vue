<script setup>
import { defineProps, ref, computed } from "vue";

const props = defineProps({
  job: Object,
});

const showFullDescription = ref(false);

const toggleFullDescription = () => {
  showFullDescription.value = !showFullDescription.value;
};

const truncatedDescription = computed(() => {
  let description = props.job.description;
  if (!showFullDescription.value) {
    description = description.substring(0, 90) + "...";
  }
  return description;
});
</script>

<template>
  <div class="bg-white rounded-xl shadow-md relative">
    <div class="p-4">
      <div class="mb-6">
        <div class="text-gray-600 my-2">{{ job.type }}</div>
        <h3 class="text-xl font-bold">{{ job.title }}</h3>
      </div>

      <div class="mb-5 space-y-2">
        <div>
          {{ truncatedDescription }}
        </div>
        <button
          class="text-blue-500 hover:text-blue-600"
          @click="toggleFullDescription"
        >
          {{ showFullDescription ? "Ver menos" : "Ver mais" }}
        </button>
      </div>

      <h3 class="text-green-500 mb-2">{{ job.salary }}</h3>

      <div class="border border-gray-100 mb-5"></div>

      <div class="flex flex-col lg:flex-row justify-between mb-4">
        <div class="text-blue-700 mb-3 flex items-center gap-2">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="20"
            height="20"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="lucide lucide-map-pin"
            aria-hidden="true"
          >
            <path
              d="M20 10c0 4.993-5.539 10.193-7.399 11.799a1 1 0 0 1-1.202 0C9.539 20.193 4 14.993 4 10a8 8 0 0 1 16 0"
            />
            <circle cx="12" cy="10" r="3" />
          </svg>
          {{ job.location }}
        </div>
        <a
          :href="'/jobs/' + job.id"
          class="h-[36px] bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-lg text-center text-sm"
        >
          Saber mais
        </a>
      </div>
    </div>
  </div>
</template>
