<script setup lang="ts">
import { ref, defineEmits } from 'vue'

const fileInput = ref<HTMLInputElement | null>(null)
const fileName = ref<string>('')
const emits = defineEmits(['file-uploaded'])

const handleFileUpload = (event: Event) => {
  const target = event.target as HTMLInputElement
  const file = target.files?.[0]

  if (file) {
    if (file.type !== 'application/pdf') {
      alert('Por favor, sube solo archivos PDF.')
      target.value = ''
      fileName.value = ''
      return
    }

    fileName.value = file.name
    const pdfPreviewUrl = URL.createObjectURL(file)
    emits('file-uploaded', { fileName: file.name, pdfPreviewUrl })
  } else {
    fileName.value = ''
  }
}

const triggerFileInput = () => {
  fileInput.value?.click()
}
</script>

<template>
  <div class="relative group">
    <div
      class="absolute -inset-1 bg-gradient-to-r from-blue-800 via-blue-600 to-blue-400 rounded-3xl blur-xl opacity-25 group-hover:opacity-50 transition duration-500 animate-tilt"
    ></div>

    <div
      class="relative bg-gradient-to-br from-slate-900/90 to-slate-800/90 rounded-3xl p-10 sm:p-12 border-2 border-dashed border-slate-600 hover:border-indigo-500 transition-all duration-500"
    >
      <div class="text-center">
        <!-- Animated Upload Icon -->
        <div class="relative inline-block mb-8">
          <div
            class="absolute inset-0 bg-gradient-to-r from-blue-800 to-blue-500 rounded-full blur-2xl opacity-40 animate-pulse"
          ></div>
          <div class="relative">
            <div
              class="w-32 h-32 mx-auto bg-gradient-to-br from-blue-800 to-blue-500 rounded-3xl flex items-center justify-center shadow-2xl transform group-hover:scale-110 transition-transform duration-500 animate-float"
            >
              <svg class="w-16 h-16 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"
                />
              </svg>
            </div>
          </div>
        </div>

        <h3 class="text-3xl font-bold text-white mb-4">Sube tu CV y descubre oportunidades</h3>

        <p class="text-indigo-300 text-lg mb-8 max-w-2xl mx-auto">
          Nuestra IA analizará tu experiencia, habilidades y formación para encontrar los trabajos perfectos para ti
        </p>

        <button
          @click="triggerFileInput"
          class="group/btn relative inline-flex items-center px-10 py-5 bg-gradient-to-r from-blue-800 via-blue-600 to-blue-400 text-white font-bold text-lg rounded-2xl shadow-2xl hover:shadow-blue-500/50 transition-all duration-300 transform hover:scale-105 overflow-hidden"
        >
          <span
            class="absolute inset-0 w-full h-full bg-gradient-to-r from-blue-400 via-blue-600 to-blue-800 opacity-0 group-hover/btn:opacity-100 transition-opacity duration-500"
          ></span>
          <svg
            class="relative w-6 h-6 mr-3 group-hover/btn:animate-bounce"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"
            />
          </svg>
          <span class="relative">Seleccionar archivo PDF</span>
          <span class="relative ml-2 text-2xl">→</span>
        </button>

        <input ref="fileInput" type="file" accept=".pdf" @change="handleFileUpload" class="hidden" />

        <div class="mt-8 grid grid-cols-1 sm:grid-cols-3 gap-4 max-w-3xl mx-auto">
          <div class="feature-box">
            <div
              class="w-12 h-12 mx-auto mb-3 bg-gradient-to-br from-blue-800 to-blue-500 rounded-xl flex items-center justify-center"
            >
              <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M13 10V3L4 14h7v7l9-11h-7z"
                />
              </svg>
            </div>
            <p class="text-white font-semibold">Análisis en segundos</p>
          </div>

          <div class="feature-box animation-delay-200ms">
            <div
              class="w-12 h-12 mx-auto mb-3 bg-gradient-to-br from-blue-600 to-blue-400 rounded-xl flex items-center justify-center"
            >
              <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"
                />
              </svg>
            </div>
            <p class="text-white font-semibold">100% Privado y Seguro</p>
          </div>

          <div class="feature-box animation-delay-400ms">
            <div
              class="w-12 h-12 mx-auto mb-3 bg-gradient-to-br from-blue-500 to-blue-300 rounded-xl flex items-center justify-center"
            >
              <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z"
                />
              </svg>
            </div>
            <p class="text-white font-semibold">Matches Precisos</p>
          </div>
        </div>

        <p
          v-if="fileName"
          class="mt-8 inline-flex items-center px-6 py-3 bg-gradient-to-r from-emerald-500/20 to-green-500/20 border-2 border-emerald-400 rounded-2xl text-emerald-400 font-bold backdrop-blur-sm animate-fade-in"
        >
          <svg class="w-6 h-6 mr-3 animate-bounce" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"
            />
          </svg>
          {{ fileName }}
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
@keyframes tilt {
  0%,
  100% {
    transform: rotate(0deg);
  }
  25% {
    transform: rotate(1deg);
  }
  75% {
    transform: rotate(-1deg);
  }
}
.animate-tilt {
  animation: tilt 10s ease-in-out infinite;
}
@keyframes float {
  0%,
  100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-20px);
  }
}
.animate-float {
  animation: float 3s ease-in-out infinite;
}
.feature-box {
  padding: 1.5rem;
  background: rgba(15, 23, 42, 0.5);
  border: 1px solid rgba(99, 102, 241, 0.2);
  border-radius: 1rem;
  text-align: center;
  transition: all 0.3s;
  animation: fade-in-up 0.6s ease-out;
}

.feature-box:hover {
  background: rgba(99, 102, 241, 0.1);
  border-color: rgba(99, 102, 241, 0.4);
  transform: translateY(-5px);
}

@keyframes fade-in-up {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animation-delay-200ms {
  animation-delay: 0.2s;
}

.animation-delay-400ms {
  animation-delay: 0.4s;
}

@keyframes fade-in {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.animate-fade-in {
  animation: fade-in 0.5s ease-out;
}
</style>
