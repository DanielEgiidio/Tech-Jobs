<script setup>
import { RouterLink, useRoute } from "vue-router";

const isActiveLink = (routePath) => {
  const route = useRoute();

  return route.path === routePath;
};
</script>

<template>
  <nav class="bg-[#1d72cb] border-b border-green-500">
    <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
      <div class="flex h-20 items-center justify-between">
        <div
          class="flex flex-1 items-center justify-center md:items-stretch md:justify-start"
        >
          <!-- Logo -->
          <RouterLink class="flex flex-shrink-0 items-center mr-4" to="/">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
              class="h-10 w-auto stroke-slate-100"
            >
              <path d="m13 13.5 2-2.5-2-2.5" />
              <path d="m21 21-4.3-4.3" />
              <path d="M9 8.5 7 11l2 2.5" />
              <circle cx="11" cy="11" r="8" />
            </svg>
            <span class="hidden md:block text-white text-2xl font-bold ml-2"
              >Tech Jobs</span
            >
          </RouterLink>
          <div class="md:ml-auto">
            <div class="flex space-x-2">
              <RouterLink
                to="/"
                :class="[
                  isActiveLink('/') ? 'bg-blue-800' : 'hover:bg-blue-800',
                  'text-white   hover:text-white rounded-md px-3 py-2',
                ]"
                >Home
              </RouterLink>
              <RouterLink
                to="/jobs"
                :class="[
                  isActiveLink('/jobs') ? 'bg-blue-800' : 'hover:bg-blue-800',
                  'text-white   hover:text-white rounded-md px-3 py-2',
                ]"
                >Vagas
              </RouterLink>
              <RouterLink
                to="/jobs/add"
                :class="[
                  isActiveLink('/jobs/add')
                    ? 'bg-blue-800'
                    : 'hover:bg-blue-800',
                  'text-white   hover:text-white rounded-md px-3 py-2',
                ]"
                >Adicionar vaga
              </RouterLink>
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>
