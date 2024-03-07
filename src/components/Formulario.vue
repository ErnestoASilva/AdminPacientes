<script setup>
    import { ref, reactive } from 'vue';
    import Alerta from './Alerta.vue'

    const alerta = reactive({
        tipo: '',
        mensaje: '',
    })
    
    const emit = defineEmits(['update:nombre', 'update:propietario', 'update:alta', 'update:sintomas', 
    'update:email', 'guardar-paciente']);

    const props = defineProps({
        nombre: {
            type: String,
            required: true
        },
        propietario: {
            type: String,
            required: true
        },
        alta: {
            type: String,
            required: true
        },
        sintomas: {
            type: String,
            required: true
        },
        email: {
            type: String,
            required: true
        },
    })

    const validar = () => {
        if (Object.values(props).includes('')) {
            alerta.mensaje = 'Todos los campos son obligatorios',
            alerta.tipo = 'error'
            return
        }else{
            alerta.mensaje = 'Paciente almacenado correctamente',
            alerta.tipo = 'exito'
            emit('guardar-paciente')
            setTimeout(() => {
                Object.assign(alerta,{
                    tipo: '',
                    mensaje: '',
                })
            }, 3000);
        }
    }


</script>

<template>
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">
            Seguimiento de Pacientes
        </h2>
        <p class="text-lg mt-5 text-center mb-10">
            Añade Paciente y
            <span class="text-indigo-600 font-bold">
                Administralos
            </span>
        </p>

        <Alerta
        v-if="alerta.mensaje"
        :alerta="alerta"
        />

        <form class="bg-white  shadow-md rounded-lg py-10 px-5 mb-10"
            @submit.prevent="validar"
        >

            <div class="mb-5">
                <label class="block text-gray-700 uppercase font-bold ml-1" for="mascota">
                    Nombre Mascota
                </label>
                <input  id="mascota"
                type="text"
                placeholder="Nombre de la mascota"
                class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                :value="nombre"
                @input="$emit('update:nombre', $event.target.value)"
                />
            </div>

            <div class="mb-5">
                <label class="block text-gray-700 uppercase font-bold ml-1" for="propietario">
                    Nombre Propietario
                </label>
                <input  id="propietario"
                type="text"
                placeholder="Nombre del propietario"
                class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                :value="propietario"
                @input="$emit('update:propietario', $event.target.value)"
                />
            </div>

            <div class="mb-5">
                <label class="block text-gray-700 uppercase font-bold ml-1" for="email">
                    Email
                </label>
                <input  id="email"
                type="email"
                placeholder="Email del propietario"
                class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                :value="email"
                @input="$emit('update:email', $event.target.value)"
                />
            </div>

            <div class="mb-5">
                <label class="block text-gray-700 uppercase font-bold ml-1" for="alta">
                    Alta
                </label>
                <input  id="alta"
                type="date"
                class="border-2 w-full p-2 mt-2 rounded-md"
                :value="alta"
                @input="$emit('update:alta', $event.target.value)"
                />
            </div>

            <div class="mb-5">
                <label class="block text-gray-700 uppercase font-bold ml-1" for="sintomas">
                    Sintomas
                </label>
                <textarea  id="sintomas"
                placeholder="Describe los sitomas del paciente"
                class="border-2 w-full p-2 mt-2  placeholder-gray-400 rounded-md h-40"
                :value="sintomas"
                @input="$emit('update:sintomas', $event.target.value)"
                />
            </div>

            <input
            type="submit"
            class="bg-indigo-600 w-full p-3 text-white uppercase 
            font-bold hover:bg-indigo-800 cursor-pointer transition-colors
            rounded-md"
            value="Registrar paciente"/>

        </form>
    </div>
</template>


<style lang="scss" scoped>

</style>