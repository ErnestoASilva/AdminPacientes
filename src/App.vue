<script setup>
import { ref, reactive } from 'vue'
import Header from './components/Header.vue';
import Formulario from './components/Formulario.vue';
import Paciente from './components/Paciente.vue';


const pacientes = ref([]);

const paciente = reactive({
    nombre: '',
    propietario : '',
    alta : '',
    sintomas : '',
    email : '',
});

const guardarPaciente = () => {
  pacientes.value.push({
    ...paciente});

  // paciente.nombre = '';
  // paciente.propietario = '';
  // paciente.alta = '';
  // paciente.sintomas = '';
  // paciente.email = '';

  Object.assign(paciente, {
    nombre: '',
    propietario : '',
    alta : '',
    sintomas : '',
    email : ''
  })
}

</script>

<template>
  <div class="container mx-auto mt-20">
    <Header/>
    <div class="mt-12 md:flex">
      <Formulario
        v-model:nombre="paciente.nombre"
        v-model:propietario="paciente.propietario"
        v-model:alta="paciente.alta"
        v-model:sintomas="paciente.sintomas"
        v-model:email="paciente.email"
        @guardar-paciente="guardarPaciente"
      />

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administra tus pacientes</h3>

        <div v-if="pacientes.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
            Información de
            <span class="text-indigo-600 font-bold">Pacientes</span>
          </p>
          <Paciente
            v-for="paciente in pacientes"
            :paciente="paciente"
          />
        </div>

        <p v-else class="mt-20 text-2xl text-center">
          No hay pacientes
        </p>
        
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>
