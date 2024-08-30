<script setup>
import { RouterLink } from "vue-router";
</script>

<template>
  <section class="text-center flex flex-col justify-center items-center h-96">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      width="120"
      height="120"
      viewBox="0 0 24 24"
      fill="none"
      stroke="currentColor"
      stroke-width="2"
      stroke-linecap="round"
      stroke-linejoin="round"
      class="text-red-500 my-8 mb-4"
    >
      <path
        d="m21.73 18-8-14a2 2 0 0 0-3.48 0l-8 14A2 2 0 0 0 4 21h16a2 2 0 0 0 1.73-3"
      />
      <path d="M12 9v4" />
      <path d="M12 17h.01" />
    </svg>
    <h1 class="text-6xl font-bold mb-4">404 Página não encontrada</h1>
    <p class="text-xl mb-5">Está página não existe</p>
    <RouterLink
      to="/"
      class="text-white bg-[#1d72cb] hover:bg-[#1d72cb]/85 rounded-md px-6 py-3.5 mt-4"
      >Voltar a Home</RouterLink
    >
  </section>
</template>
