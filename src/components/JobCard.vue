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
}

const props = defineProps<{
  job: JobRecommendation
  index: number
}>()

const emits = defineEmits(['view-detail'])

const getMatchColor = (percentage: number): string => {
  if (percentage >= 90) return 'from-emerald-400 to-green-500'
  if (percentage >= 85) return 'from-blue-400 to-cyan-500'
  return 'from-violet-400 to-purple-500'
}

const getMatchBorder = (percentage: number): string => {
  if (percentage >= 90) return 'border-emerald-400'
  if (percentage >= 85) return 'border-blue-400'
  return 'border-violet-400'
}

const viewDetail = () => {
  emits('view-detail', props.job.id)
}
</script>

<template>
  <div class="job-card" :style="{ animationDelay: `${index * 100}ms` }">
    <div
      class="absolute -inset-0.5 bg-gradient-to-r from-blue-800 via-blue-600 to-blue-400 rounded-3xl blur-lg opacity-0 group-hover:opacity-30 transition-all duration-500"
    ></div>

    <div class="relative glass-card rounded-3xl p-8 border border-white/10 h-full">
      <div class="flex justify-between items-start mb-6 flex-wrap gap-4">
        <div class="flex items-start space-x-4 flex-1 min-w-0">
          <div class="job-icon">
            <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
              />
            </svg>
          </div>

          <div class="flex-1 min-w-0">
            <h3
              class="text-2xl font-bold text-white mb-2 group-hover:text-indigo-400 transition-colors truncate"
            >
              {{ job.title }}
            </h3>

            <div class="flex flex-wrap gap-3 mb-3">
              <span class="job-meta">
                <svg
                  class="w-4 h-4 text-indigo-400"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4"
                  />
                </svg>
                {{ job.company }}
              </span>

              <span class="job-meta">
                <svg
                  class="w-4 h-4 text-purple-400"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"
                  />
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
                  />
                </svg>
                {{ job.location }}
              </span>

              <span class="job-meta" v-if="job.salary">
                <svg
                  class="w-4 h-4 text-emerald-400"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
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

            <p class="text-slate-300 line-clamp-2 text-sm">
              {{ job.description }}
            </p>
          </div>
        </div>

        <!-- Match Badge -->
        <div class="relative flex-shrink-0">
          <div
            :class="[
              'absolute inset-0 rounded-2xl blur-xl opacity-60 animate-pulse',
              getMatchColor(job.matchPercentage)
            ]"
          ></div>
          <div
            :class="[
              'relative px-6 py-4 rounded-2xl font-black text-lg border-2 shadow-2xl bg-slate-900/50 backdrop-blur-sm',
              getMatchBorder(job.matchPercentage)
            ]"
          >
            <div
              :class="[
                'text-2xl mb-1 bg-gradient-to-r bg-clip-text text-transparent',
                getMatchColor(job.matchPercentage)
              ]"
            >
              {{ job.matchPercentage }}%
            </div>
            <div class="text-xs text-slate-400 font-semibold">MATCH</div>
          </div>
        </div>
      </div>

      <!-- Tags -->
      <div class="flex flex-wrap gap-2 mb-6" v-if="job.requirements">
        <span v-for="req in job.requirements.slice(0, 4)" :key="req" class="skill-tag">
          {{ req }}
        </span>
      </div>

      <!-- Action Button -->
      <button @click="viewDetail" class="action-btn">
        <span class="relative z-10 flex items-center">
          Ver Detalles Completos
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
</template>

<style scoped>
/* Glass Effect */
.glass-card {
  background: rgba(15, 23, 42, 0.7);
  backdrop-filter: blur(20px);
}

.job-card {
  position: relative;
  animation: fade-in-up 0.6s ease-out;
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

.job-card .group:hover {
  transform: translateY(-5px);
}

.job-icon {
  width: 4rem;
  height: 4rem;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #1e40af, #3b82f6);
  border-radius: 1rem;
  flex-shrink: 0;
  box-shadow: 0 10px 25px -5px rgba(99, 102, 241, 0.5);
}

.job-meta {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem 1rem;
  background: rgba(99, 102, 241, 0.1);
  border: 1px solid rgba(99, 102, 241, 0.2);
  border-radius: 0.75rem;
  font-size: 0.875rem;
  font-weight: 600;
  color: rgb(203, 213, 225);
  backdrop-filter: blur(10px);
}

.skill-tag {
  padding: 0.5rem 1rem;
  background: rgba(139, 92, 246, 0.1);
  border: 1px solid rgba(139, 92, 246, 0.3);
  border-radius: 0.5rem;
  font-size: 0.75rem;
  font-weight: 600;
  color: rgb(196, 181, 253);
  transition: all 0.3s;
}

.skill-tag:hover {
  background: rgba(139, 92, 246, 0.2);
  border-color: rgba(139, 92, 246, 0.5);
  transform: translateY(-2px);
}

.action-btn {
  position: relative;
  width: 100%;
  padding: 1rem 2rem;
  background: linear-gradient(135deg, #1e40af, #3b82f6, #60a5fa);
  background-size: 200% 200%;
  color: white;
  font-weight: 700;
  border-radius: 1rem;
  overflow: hidden;
  transition: all 0.3s;
  border: none;
  cursor: pointer;
}

.action-btn:hover {
  background-position: 100% 0;
  box-shadow: 0 20px 40px -10px rgba(99, 102, 241, 0.6);
  transform: translateY(-2px);
}

.action-btn::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transform: translateX(-100%);
  transition: transform 0.6s;
}

.action-btn:hover::before {
  transform: translateX(100%);
}

/* Line Clamp */
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>
