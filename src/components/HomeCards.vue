<script setup>
import Card from "./Card.vue";
</script>

<template>
  <section class="py-4">
    <div class="container-xl lg:container m-auto">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4 p-4 rounded-lg">
        <Card>
          <h2 class="text-2xl font-bold">Para Desenvolvedores</h2>
          <p class="mt-2 mb-4">Encontre a sua esperada oportunidade hoje.</p>
          <a
            href="jobs.html"
            class="inline-block bg-black text-white rounded-lg px-4 py-2 hover:bg-gray-700"
          >
            Buscar jobs
          </a>
        </Card>
        <Card bg="bg-[#1d72cb]/20">
          <h2 class="text-2xl font-bold">Para empresas</h2>
          <p class="mt-2 mb-4">
            Cadastre a vaga para encontrar o desenvolvedor ideal.
          </p>
          <a
            href="add-job.html"
            class="inline-block bg-[#1d72cb] text-white rounded-lg px-4 py-2 hover:bg-[#1d72cb]/85"
          >
            Adicionar jobs
          </a>
        </Card>
      </div>
    </div>
  </section>
</template>
