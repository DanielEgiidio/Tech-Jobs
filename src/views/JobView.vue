<script setup>
import { reactive, onMounted } from "vue";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";
import axios from "axios";
import { useRoute, RouterLink, useRouter } from "vue-router";
import BackButton from "@/components/BackButton.vue";
import { useToast } from "vue-toastification";

const route = useRoute();
const router = useRouter();
const toast = useToast();

const jobId = route.params.id;
const state = reactive({
  job: {},
  isLoading: true,
});

const deleteJob = async () => {
  try {
    const confirm = window.confirm("Tem certeza que quer excluir essa vaga ?");
    if (confirm) {
      await axios.delete(`/api/jobs/${jobId}`);
      toast.success("Vaga deletada com sucesso");
      router.push("/jobs");
    }
  } catch (error) {
    console.error("Erro ao deletar vaga", error);
    toast.error("Erro ao deletar vaga ");
  }
};

onMounted(async () => {
  try {
    const response = await axios.get(`/api/jobs/${jobId}`);
    state.job = response.data;
  } catch (error) {
    console.error("Erro ao tentar acessar a vaga:", error);
  } finally {
    state.isLoading = false;
  }
});
</script>

<template>
  <BackButton />
  <section v-if="!state.isLoading" class="bg-blue-50">
    <div class="container m-auto py-10 px-6">
      <div class="grid grid-cols-1 md:grid-cols-70/30 w-full gap-6">
        <main>
          <div
            class="bg-white p-6 rounded-lg shadow-md text-center md:text-left"
          >
            <div class="text-gray-500 mb-4">{{ state.job.type }}</div>
            <h1 class="text-3xl font-bold mb-4">{{ state.job.title }}</h1>
            <div
              class="text-gray-500 mb-4 flex align-middle justify-center md:justify-start"
            >
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
              <p class="text-blue-700">{{ state.job.location }}</p>
            </div>
          </div>

          <div class="bg-white p-6 rounded-lg shadow-md mt-6">
            <h3 class="text-blue-800 text-lg font-bold mb-6">
              Descrição da vaga
            </h3>

            <p class="mb-4 leading-snug">
              {{ state.job.description }}
            </p>

            <h3 class="text-blue-800 text-lg font-bold mb-2">Salário</h3>

            <p class="mb-4 text-green-800 font-bold tracking-wide">
              {{ state.job.salary }}
            </p>
          </div>
        </main>

        <!-- Sidebar -->
        <aside>
          <!-- Company Info -->
          <div class="bg-white p-6 rounded-lg shadow-md">
            <h3 class="text-xl font-bold mb-6">Informação da Empresa</h3>

            <h2 class="text-2xl">{{ state.job.company.name }}</h2>

            <p class="my-2 leading-snug">
              {{ state.job.company.description }}
            </p>

            <hr class="my-4" />

            <h3 class="text-xl">Email:</h3>

            <p class="my-2 bg-blue-100 p-2 font-bold">
              {{ state.job.company.contactEmail }}
            </p>

            <h3 class="text-xl">Telefone:</h3>

            <p class="my-2 bg-blue-100 p-2 font-bold">
              {{ state.job.company.contactPhone }}
            </p>
          </div>

          <!-- Manage -->
          <div class="bg-white p-6 rounded-lg shadow-md mt-6">
            <h3 class="text-xl font-bold mb-6">Gerenciar vaga</h3>
            <RouterLink
              :to="`/jobs/edit/${state.job.id}`"
              class="bg-green-500 hover:bg-green-600 text-white text-center font-bold py-3 px-4 rounded-full w-full focus:outline-none focus:shadow-outline mt-4 block"
              >Editar vaga
            </RouterLink>
            <button
              @click="deleteJob"
              class="bg-red-500 hover:bg-red-600 text-white font-bold py-3 px-4 rounded-full w-full focus:outline-none focus:shadow-outline mt-4 block"
            >
              Deletar vaga
            </button>
          </div>
        </aside>
      </div>
    </div>
  </section>
  <div v-else class="text-center text-blue-500 py-6">
    <PulseLoader />
  </div>
</template>
