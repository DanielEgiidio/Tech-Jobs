<script setup>
import logo from "@/assets/images/logo.png";
</script>

<template>
  <nav class="bg-[#1d72cb] border-b border-green-500">
    <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
      <div class="flex h-20 items-center justify-between">
        <div
          class="flex flex-1 items-center justify-center md:items-stretch md:justify-start"
        >
          <!-- Logo -->
          <a class="flex flex-shrink-0 items-center mr-4" href="index.html">
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
          </a>
          <div class="md:ml-auto">
            <div class="flex space-x-2">
              <a
                href="/"
                class="text-white bg-blue-800 hover:bg-blue-800 hover:text-white rounded-md px-3 py-2"
                >Home</a
              >
              <a
                href="#jobs"
                class="text-white hover:bg-blue-800 hover:text-white rounded-md px-3 py-2"
                >Vagas</a
              >
              <a
                href="/"
                class="text-white hover:bg-blue-800 hover:text-white rounded-md px-3 py-2"
                >Adicionar vaga</a
              >
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>
