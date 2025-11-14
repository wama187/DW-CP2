<script setup lang="ts">
import { defineProps, defineEmits } from 'vue'

interface JobRecommendation {
  id: number
  title: string
  company: string
  location: string
  matchPercentage: number
  description: string
  salary?: string
  requirements?: string[]
  benefits?: string[]
}

defineProps<{
  job: JobRecommendation | null
}>()

const emits = defineEmits(['close'])

const closeModal = () => {
  emits('close')
}
</script>

<template>
  <div
    class="fixed inset-0 bg-black/80 backdrop-blur-md z-50 flex justify-center items-center p-4 animate-fade-in"
    @click.self="closeModal"
  >
    <div v-if="job" class="modal-content">
      <div
        class="absolute -inset-1 bg-gradient-to-r from-blue-800 via-blue-600 to-blue-400 rounded-3xl blur-2xl opacity-30"
      ></div>

      <div
        class="relative bg-slate-900 rounded-3xl shadow-2xl max-w-4xl w-full mx-auto overflow-hidden border border-white/10"
      >
        <!-- Modal Header -->
        <div class="relative bg-gradient-to-r from-blue-800 via-blue-600 to-blue-400 px-8 py-10 overflow-hidden">
          <div class="absolute inset-0 bg-black/20"></div>
          <div class="absolute inset-0 bg-grid-pattern opacity-10"></div>

          <div class="relative z-10">
            <div class="flex items-start justify-between mb-6">
              <div class="flex items-start space-x-4 flex-1">
                <div
                  class="w-20 h-20 bg-white/20 backdrop-blur-lg rounded-2xl flex items-center justify-center shadow-2xl"
                >
                  <svg class="w-10 h-10 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
                    />
                  </svg>
                </div>

                <div class="flex-1">
                  <h2 class="text-4xl font-black text-white mb-3 leading-tight">
                    {{ job.title }}
                  </h2>
                  <div class="flex flex-wrap gap-3 text-white/90">
                    <span class="flex items-center font-semibold">
                      <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4"
                        />
                      </svg>
                      {{ job.company }}
                    </span>
                    <span class="flex items-center">
                      <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"
                        />
                      </svg>
                      {{ job.location }}
                    </span>
                    <span class="flex items-center" v-if="job.salary">
                      <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
                        />
                      </svg>
                      {{ job.salary }}
                    </span>
                  </div>
                </div>
              </div>

              <button
                @click="closeModal"
                class="w-12 h-12 bg-white/20 hover:bg-white/30 backdrop-blur-lg rounded-xl flex items-center justify-center transition-all duration-200 transform hover:scale-110 hover:rotate-90 flex-shrink-0"
              >
                <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                </svg>
              </button>
            </div>

            <!-- Match Score -->
            <div
              class="inline-flex items-center bg-white/20 backdrop-blur-lg rounded-2xl px-6 py-3 border border-white/30"
            >
              <div class="flex items-center space-x-3">
                <div class="relative w-16 h-16">
                  <svg class="w-16 h-16 transform -rotate-90">
                    <circle
                      cx="32"
                      cy="32"
                      r="28"
                      stroke="rgba(255,255,255,0.2)"
                      stroke-width="4"
                      fill="none"
                    />
                    <circle
                      cx="32"
                      cy="32"
                      r="28"
                      stroke="white"
                      stroke-width="4"
                      fill="none"
                      :stroke-dasharray="`${job.matchPercentage * 1.76} 176`"
                      class="transition-all duration-1000"
                    />
                  </svg>
                  <div class="absolute inset-0 flex items-center justify-center text-white font-bold text-sm">
                    {{ job.matchPercentage }}%
                  </div>
                </div>
                <div class="text-white">
                  <div class="font-black text-xl">Match Perfecto</div>
                  <div class="text-white/80 text-sm">Altamente compatible</div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Modal Body -->
        <div class="p-8 space-y-8 max-h-[60vh] overflow-y-auto custom-scrollbar">
          <!-- Description -->
          <div class="space-y-4">
            <h3 class="text-2xl font-black text-white flex items-center">
              <div class="w-1.5 h-8 bg-gradient-to-b from-blue-800 to-blue-500 rounded-full mr-4"></div>
              Descripción del puesto
            </h3>
            <p class="text-slate-300 leading-relaxed text-lg pl-6">
              {{ job.description }}
            </p>
          </div>

          <!-- Requirements -->
          <div class="space-y-4" v-if="job.requirements">
            <h3 class="text-2xl font-black text-white flex items-center">
              <div class="w-1.5 h-8 bg-gradient-to-b from-blue-600 to-blue-400 rounded-full mr-4"></div>
              Requisitos
            </h3>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-3 pl-6">
              <div
                v-for="req in job.requirements"
                :key="req"
                class="flex items-center space-x-3 bg-slate-800/50 rounded-xl p-3 border border-slate-700"
              >
                <div class="w-2 h-2 bg-gradient-to-br from-blue-800 to-blue-500 rounded-full"></div>
                <span class="text-slate-200 font-medium">{{ req }}</span>
              </div>
            </div>
          </div>

          <!-- Benefits -->
          <div class="space-y-4" v-if="job.benefits">
            <h3 class="text-2xl font-black text-white flex items-center">
              <div class="w-1.5 h-8 bg-gradient-to-b from-blue-500 to-blue-300 rounded-full mr-4"></div>
              Beneficios
            </h3>
            <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 pl-6">
              <div v-for="benefit in job.benefits" :key="benefit" class="benefit-card">
                <svg class="w-6 h-6 text-emerald-400 mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                </svg>
                <span class="text-slate-200 font-semibold text-sm">{{ benefit }}</span>
              </div>
            </div>
          </div>

          <!-- AI Insights -->
          <div class="relative">
            <div
              class="absolute -inset-1 bg-gradient-to-r from-blue-800 to-blue-500 rounded-2xl blur-xl opacity-20"
            ></div>
            <div class="relative glass-card rounded-2xl p-6 border border-indigo-500/30">
              <div class="flex items-start space-x-4">
                <div
                  class="w-12 h-12 bg-gradient-to-br from-blue-800 to-blue-500 rounded-xl flex items-center justify-center flex-shrink-0"
                >
                  <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"
                    />
                  </svg>
                </div>
                <div>
                  <h4 class="text-white font-bold text-lg mb-2">Análisis IA</h4>
                  <p class="text-indigo-300 text-sm leading-relaxed">
                    Tu perfil coincide especialmente en habilidades técnicas y experiencia relevante. Este puesto se
                    alinea perfectamente con tu trayectoria profesional.
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Modal Footer -->
        <div class="p-8 bg-slate-800/50 border-t border-slate-700">
          <div class="flex flex-col sm:flex-row justify-between items-center gap-4">
            <button
              @click="closeModal"
              class="w-full sm:w-auto px-8 py-4 bg-slate-700 hover:bg-slate-600 text-white font-bold rounded-xl transition-all duration-200 transform hover:scale-105"
            >
              Cerrar
            </button>

            <div class="flex gap-3 w-full sm:w-auto">
              <button
                class="flex-1 sm:flex-none px-8 py-4 bg-slate-700 hover:bg-slate-600 text-white font-bold rounded-xl transition-all duration-200 transform hover:scale-105 flex items-center justify-center"
              >
                <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M5 5a2 2 0 012-2h10a2 2 0 012 2v16l-7-3.5L5 21V5z"
                  />
                </svg>
                Guardar
              </button>

              <button
                class="flex-1 sm:flex-none relative px-8 py-4 bg-gradient-to-r from-blue-800 via-blue-600 to-blue-400 hover:from-blue-400 hover:via-blue-600 hover:to-blue-800 text-white font-bold rounded-xl transition-all duration-300 transform hover:scale-105 shadow-2xl flex items-center justify-center group overflow-hidden"
              >
                <span
                  class="absolute inset-0 w-full h-full bg-gradient-to-r from-white/20 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"
                ></span>
                <span class="relative flex items-center">
                  Aplicar Ahora
                  <svg
                    class="w-5 h-5 ml-2 group-hover:translate-x-1 transition-transform"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7l5 5m0 0l-5 5m5-5H6" />
                  </svg>
                </span>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Custom Scrollbar */
.custom-scrollbar::-webkit-scrollbar {
  width: 8px;
}

.custom-scrollbar::-webkit-scrollbar-track {
  background: rgba(51, 65, 85, 0.3);
  border-radius: 10px;
}

.custom-scrollbar::-webkit-scrollbar-thumb {
  background: linear-gradient(180deg, #1e40af, #3b82f6);
  border-radius: 10px;
}

.custom-scrollbar::-webkit-scrollbar-thumb:hover {
  background: linear-gradient(180deg, #1d4ed8, #2563eb);
}

.modal-content {
  animation: modal-scale-in 0.3s ease-out;
}

@keyframes modal-scale-in {
  from {
    opacity: 0;
    transform: scale(0.95);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
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

.benefit-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1.5rem;
  background: rgba(16, 185, 129, 0.1);
  border: 1px solid rgba(16, 185, 129, 0.3);
  border-radius: 1rem;
  text-align: center;
  transition: all 0.3s;
}

.benefit-card:hover {
  background: rgba(16, 185, 129, 0.2);
  border-color: rgba(16, 185, 129, 0.5);
  transform: translateY(-5px);
}

.bg-grid-pattern {
  background-image: linear-gradient(rgba(59, 130, 246, 0.1) 1px, transparent 1px),
    linear-gradient(90deg, rgba(59, 130, 246, 0.1) 1px, transparent 1px);
  background-size: 50px 50px;
}
</style>
