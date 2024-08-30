<script setup>
import { reactive, onMounted } from "vue";
import { useRoute } from "vue-router";
import router from "@/router";
import axios from "axios";
import { useToast } from "vue-toastification";

const route = useRoute();

const jobId = route.params.id;

const form = reactive({
  type: "Tempo Integral",
  title: "",
  description: "",
  salary: "",
  location: "",
  company: {
    name: "",
    description: "",
    contactEmail: "",
    contactPhone: "",
  },
});

const toast = useToast();

const state = reactive({
  job: {},
  isLoading: true,
});

const handleSubmit = async () => {
  const updatedJob = {
    title: form.title,
    type: form.type,
    location: form.location,
    description: form.description,
    salary: form.salary,
    company: {
      name: form.company.name,
      description: form.company.description,
      contactEmail: form.company.contactEmail,
      contactPhone: form.company.contactPhone,
    },
  };

  try {
    const response = await axios.put(`/api/jobs/${jobId}`, updatedJob);
    toast.success("Vaga editada com sucesso");
    router.push(`/jobs/${response.data.id}`);
  } catch (error) {
    console.error("Error ao editar a vaga", error);
    toast.error("A vaga não foi editada");
  }
};

onMounted(async () => {
  try {
    const response = await axios.get(`/api/jobs/${jobId}`);
    state.job = response.data;

    form.type = state.job.type;
    form.title = state.job.title;
    form.description = state.job.description;
    form.salary = state.job.salary;
    form.location = state.job.location;
    form.company.name = state.job.company.name;
    form.company.description = state.job.company.description;
    form.company.contactEmail = state.job.company.contactEmail;
    form.company.contactPhone = state.job.company.contactPhone;
  } catch (error) {
    console.error("Error fetching vaga", error);
  } finally {
    state.isLoading = false;
  }
});
</script>

<template>
  <section class="bg-blue-50">
    <div class="container m-auto max-w-2xl py-24">
      <div
        class="bg-white px-6 py-8 mb-4 shadow-md rounded-md border m-4 md:m-0"
      >
        <form @submit.prevent="handleSubmit">
          <h2 class="text-3xl text-center font-semibold mb-6">Editar vaga</h2>

          <div class="mb-4">
            <label for="type" class="block text-gray-700 font-bold mb-2"
              >Tipo da vaga</label
            >
            <select
              v-model="form.type"
              id="type"
              name="type"
              class="border rounded w-full py-2 px-3"
              required
            >
              <option value="Tempo Integral">Tempo Integral</option>
              <option value="Meio Período">Meio Período</option>
              <option value="Remoto">Remoto</option>
              <option value="Estágio">Estágio</option>
            </select>
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2"
              >Nome da vaga</label
            >
            <input
              type="text"
              v-model="form.title"
              id="title"
              name="title"
              class="border rounded w-full py-2 px-3 mb-2"
              placeholder="Desenvolvedor Backend"
              required
            />
          </div>
          <div class="mb-4">
            <label for="description" class="block text-gray-700 font-bold mb-2"
              >Descrição da vaga</label
            >
            <textarea
              id="description"
              v-model="form.description"
              name="description"
              class="border rounded w-full py-2 px-3"
              rows="4"
              placeholder="Adiciona as funções da vaga, expectativas, requisitos, etc"
            ></textarea>
          </div>

          <div class="mb-4">
            <label for="salary" class="block text-gray-700 font-bold mb-2"
              >Salário</label
            >
            <input
              type="text"
              v-model="form.salary"
              id="salary"
              name="salary"
              class="border rounded w-full py-2 px-3"
              placeholder="R$7.000 - R$8.000/mês"
              required
            />
          </div>

          <div class="mb-4">
            <label class="block text-gray-700 font-bold mb-2">
              Localização
            </label>
            <input
              type="text"
              v-model="form.location"
              id="location"
              name="location"
              class="border rounded w-full py-2 px-3 mb-2"
              placeholder="Campinas, São Paulo"
              required
            />
          </div>

          <h3 class="text-2xl mb-5">Informações da empresa</h3>

          <div class="mb-4">
            <label for="company" class="block text-gray-700 font-bold mb-2"
              >Nome da empresa</label
            >
            <input
              type="text"
              v-model="form.company.name"
              id="company"
              name="company"
              class="border rounded w-full py-2 px-3"
              placeholder="Nome da empresa"
            />
          </div>

          <div class="mb-4">
            <label
              for="company_description"
              class="block text-gray-700 font-bold mb-2"
              >Descrição da empresa</label
            >
            <textarea
              id="company_description"
              v-model="form.company.description"
              name="company_description"
              class="border rounded w-full py-2 px-3"
              rows="4"
              placeholder="O que a empresa faz?"
            ></textarea>
          </div>

          <div class="mb-4">
            <label
              for="contact_email"
              class="block text-gray-700 font-bold mb-2"
              >Email para contato</label
            >
            <input
              type="email"
              v-model="form.company.contactEmail"
              id="contact_email"
              name="contact_email"
              class="border rounded w-full py-2 px-3"
              placeholder="Endereço de email para os candidatos"
              required
            />
          </div>
          <div class="mb-4">
            <label
              for="contact_phone"
              class="block text-gray-700 font-bold mb-2"
              >Telefone para contato</label
            >
            <input
              type="tel"
              v-model="form.company.contactPhone"
              id="contact_phone"
              name="contact_phone"
              class="border rounded w-full py-2 px-3"
              placeholder="(11) 91234-5678"
            />
          </div>

          <div>
            <button
              class="bg-blue-500 hover:bg-blue-600 text-white font-bold py-3 px-4 rounded-lg w-full focus:outline-none focus:shadow-outline"
              type="submit"
            >
              Editar Vaga
            </button>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>
