<script setup lang="ts">
import { defineProps, defineEmits } from 'vue'
import JobCard from './JobCard.vue'

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
  jobRecommendations: JobRecommendation[]
  skillsExtracted: number
}>()

const emits = defineEmits(['view-detail'])

const viewDetail = (jobId: number) => {
  emits('view-detail', jobId)
}
</script>

<template>
  <div class="mt-12 space-y-8 animate-fade-in">
    <!-- Success Banner -->
    <div class="relative group/success">
      <div
        class="absolute -inset-1 bg-gradient-to-r from-emerald-600 to-green-600 rounded-2xl blur-xl opacity-40 group-hover/success:opacity-60 transition duration-500"
      ></div>
      <div class="relative glass-card rounded-2xl p-8 border border-emerald-500/30">
        <div class="flex items-center justify-between flex-wrap gap-4">
          <div class="flex items-center space-x-4">
            <div
              class="w-16 h-16 bg-gradient-to-br from-emerald-500 to-green-500 rounded-2xl flex items-center justify-center shadow-2xl animate-bounce-slow"
            >
              <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"
                />
              </svg>
            </div>
            <div>
              <h3 class="text-2xl font-bold text-white mb-1">¡Análisis completado con éxito!</h3>
              <p class="text-emerald-400 font-semibold text-lg">{{ skillsExtracted }} habilidades clave identificadas</p>
            </div>
          </div>

          <div class="flex gap-3">
            <div class="stat-box">
              <div class="text-3xl font-black text-white">{{ jobRecommendations.length }}</div>
              <div class="text-indigo-300 text-sm font-semibold">Ofertas</div>
            </div>
            <div class="stat-box">
              <div class="text-3xl font-black text-white">98%</div>
              <div class="text-purple-300 text-sm font-semibold">Precisión</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Jobs Header -->
    <div class="flex items-center justify-between flex-wrap gap-4">
      <h2 class="text-4xl font-black text-white flex items-center">

        Tus mejores opciones de trabajo
      </h2>
    </div>

    <!-- Job Cards -->
    <div class="grid gap-6">
      <JobCard
        v-for="(job, index) in jobRecommendations"
        :key="job.id"
        :job="job"
        :index="index"
        @view-detail="viewDetail"
      />
    </div>
  </div>
</template>

<style scoped>
.glass-card {
  background: rgba(15, 23, 42, 0.7);
  backdrop-filter: blur(20px);
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
@keyframes bounce-slow {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}
.animate-bounce-slow {
  animation: bounce-slow 2s ease-in-out infinite;
}
.stat-box {
  padding: 1rem 1.5rem;
  background: rgba(99, 102, 241, 0.1);
  border: 1px solid rgba(99, 102, 241, 0.3);
  border-radius: 1rem;
  text-align: center;
  backdrop-filter: blur(10px);
}
.filter-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  background: rgba(99, 102, 241, 0.1);
  border: 1px solid rgba(99, 102, 241, 0.3);
  color: white;
  font-weight: 600;
  border-radius: 0.75rem;
  transition: all 0.3s;
  backdrop-filter: blur(10px);
}

.filter-btn:hover {
  background: rgba(99, 102, 241, 0.2);
  border-color: rgba(99, 102, 241, 0.5);
  transform: translateY(-2px);
}
</style>
