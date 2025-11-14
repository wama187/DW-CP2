<script setup lang="ts">
import { ref } from 'vue'
import FileUpload from './FileUpload.vue'
import AnalyzingIndicator from './AnalyzingIndicator.vue'
import Results from './Results.vue'
import JobDetailModal from './JobDetailModal.vue'

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

const fileName = ref<string>('')
const pdfPreviewUrl = ref<string>('')
const showResults = ref<boolean>(false)
const isAnalyzing = ref<boolean>(false)
const skillsExtracted = ref<number>(8)
const isModalOpen = ref<boolean>(false)
const selectedJob = ref<JobRecommendation | null>(null)

const jobRecommendations = ref<JobRecommendation[]>([
  {
    id: 1,
    title: 'Desarrollador Full-Stack Senior',
    company: 'TechCorp Solutions',
    location: 'Madrid, España',
    matchPercentage: 92,
    salary: '€55,000 - €75,000',
    description:
      'Buscamos un desarrollador Full-Stack Senior con experiencia en Vue.js y Node.js para unirse a nuestro equipo. Serás responsable de diseñar, desarrollar y mantener nuestras aplicaciones web.',
    requirements: ['5+ años de experiencia', 'Vue.js & React', 'Node.js', 'MongoDB'],
    benefits: ['Trabajo remoto', 'Seguro médico', 'Formación continua']
  },
  {
    id: 2,
    title: 'Ingeniero de Software Vue.js',
    company: 'Innovative Systems',
    location: 'Barcelona, España (Remoto)',
    matchPercentage: 88,
    salary: '€45,000 - €65,000',
    description:
      'Estamos buscando un ingeniero de software especializado en Vue.js para trabajar en proyectos innovadores. Se requiere experiencia en el desarrollo de aplicaciones de una sola página (SPA).',
    requirements: ['3+ años con Vue.js', 'TypeScript', 'Testing', 'Git'],
    benefits: ['Horario flexible', 'Bonus anual', 'Team building']
  },
  {
    id: 3,
    title: 'Especialista en Frontend',
    company: 'Digital Ventures',
    location: 'Valencia, España',
    matchPercentage: 85,
    salary: '€40,000 - €55,000',
    description:
      'Únete a nuestro equipo como especialista en Frontend y trabaja con las últimas tecnologías. Es necesario tener un sólido conocimiento de HTML, CSS y JavaScript.',
    requirements: ['HTML5/CSS3', 'JavaScript ES6+', 'Responsive Design', 'Figma'],
    benefits: ['Jornada intensiva verano', 'Clases de inglés', 'Gym pass']
  },
  {
    id: 4,
    title: 'Arquitecto de Soluciones Web',
    company: 'CloudTech Inc.',
    location: 'Remoto',
    matchPercentage: 82,
    salary: '€60,000 - €85,000',
    description:
      'Buscamos un arquitecto de soluciones web para diseñar y supervisar la implementación de soluciones escalables en la nube. Se requiere experiencia con AWS o Azure.',
    requirements: ['AWS/Azure', 'Microservicios', 'Docker/Kubernetes', 'CI/CD'],
    benefits: ['100% remoto', 'Días libres ilimitados', 'Stock options']
  }
])

const onFileUploaded = (payload: { fileName: string; pdfPreviewUrl: string }) => {
  fileName.value = payload.fileName
  pdfPreviewUrl.value = payload.pdfPreviewUrl
  isAnalyzing.value = true
  showResults.value = false

  setTimeout(() => {
    isAnalyzing.value = false
    showResults.value = true
  }, 20000)
}

const viewDetail = (jobId: number) => {
  const job = jobRecommendations.value.find((j) => j.id === jobId)
  if (job) {
    selectedJob.value = job
    isModalOpen.value = true
  }
}

const closeModal = () => {
  isModalOpen.value = false
  selectedJob.value = null
}
</script>

<template>
  <div
    class="min-h-screen bg-gradient-to-br from-slate-950 via-blue-950 to-blue-800 py-8 px-4 sm:px-6 lg:px-8 relative overflow-hidden"
  >
    <!-- Animated Background Elements -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div class="absolute top-0 left-1/4 w-96 h-96 bg-blue-800/20 rounded-full blur-3xl animate-pulse-slow"></div>
      <div
        class="absolute bottom-0 right-1/4 w-96 h-96 bg-blue-600/20 rounded-full blur-3xl animate-pulse-slow animation-delay-2s"
      ></div>
      <div
        class="absolute top-1/2 left-1/2 w-96 h-96 bg-blue-400/10 rounded-full blur-3xl animate-pulse-slow animation-delay-4s"
      ></div>

      <!-- Grid Pattern -->
      <div class="absolute inset-0 bg-grid-pattern opacity-5"></div>


    </div>

    <div class="max-w-7xl mx-auto relative z-10">
      <!-- Hero Header -->
      <div class="text-center mb-12 animate-fade-in-down">
        <div class="inline-flex items-center justify-center mb-6">
          <div class="relative">
            <div
              class="absolute inset-0 bg-gradient-to-r from-blue-800 via-blue-600 to-blue-400 rounded-full blur-2xl opacity-50 animate-spin-slow"
            ></div>
            <div class="relative bg-gradient-to-br from-blue-800 to-blue-500 rounded-3xl p-5 shadow-2xl">
              <svg class="w-16 h-16 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M13 10V3L4 14h7v7l9-11h-7z"
                />
              </svg>
            </div>
          </div>
        </div>

        <h1 class="text-6xl sm:text-7xl font-black mb-6 leading-tight">
          <span
            class="bg-gradient-to-r from-blue-500 via-blue-400 to-blue-300 bg-clip-text text-transparent animate-gradient"
          >
            IntelliJob
          </span>
          <span class="text-white block mt-2">Plataforma de busqueda de empleo</span>
        </h1>

        <p class="text-xl sm:text-2xl text-blue-200 font-medium max-w-3xl mx-auto mb-8">
          Análisis inteligente de CV con
          <span class="text-blue-400 font-bold">IA Generativa</span> y
          <span class="text-blue-300 font-bold">NLP avanzado</span>
        </p>

        <div class="flex flex-wrap justify-center gap-3 mb-8">
          <div class="badge-tech">
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"
              />
            </svg>
            Machine Learning
          </div>
          <div class="badge-tech animation-delay-200ms">
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M7 8h10M7 12h4m1 8l-4-4H5a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v8a2 2 0 01-2 2h-3l-4 4z"
              />
            </svg>
            Natural Language Processing
          </div>
          <div class="badge-tech animation-delay-400ms">
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6" />
            </svg>
            Smart Matching 98%
          </div>
        </div>
      </div>

      <!-- Main Content Card -->
      <div class="glass-card rounded-3xl overflow-hidden shadow-2xl border border-white/10 animate-fade-in-up">
        <!-- Upload Section -->
        <div class="p-8 sm:p-12">
          <FileUpload @file-uploaded="onFileUploaded" />

          <!-- PDF Preview -->
          <div v-if="pdfPreviewUrl" class="mt-12 animate-fade-in">
            <div class="flex items-center justify-between mb-6">
              <h3 class="text-3xl font-bold text-white flex items-center">
                <div class="w-2 h-10 bg-gradient-to-b from-blue-800 to-blue-500 rounded-full mr-4"></div>
                Vista previa del documento
              </h3>
              <div
                class="px-4 py-2 bg-blue-500/20 border border-blue-400 rounded-xl text-blue-400 font-semibold backdrop-blur-sm"
              >
                Procesando...
              </div>
            </div>
            <div class="relative group/preview">
              <div
                class="absolute -inset-1 bg-gradient-to-r from-blue-800 to-blue-500 rounded-2xl blur-xl opacity-25 group-hover/preview:opacity-40 transition duration-500"
              ></div>
              <iframe
                :src="pdfPreviewUrl"
                class="relative w-full h-[700px] rounded-2xl border-2 border-slate-700 shadow-2xl bg-white"
              ></iframe>
            </div>
          </div>

          <AnalyzingIndicator v-if="isAnalyzing" />

          <Results
            v-if="showResults"
            :job-recommendations="jobRecommendations"
            :skills-extracted="skillsExtracted"
            @view-detail="viewDetail"
          />
        </div>
      </div>

      <!-- Footer -->
      <div class="mt-12 text-center animate-fade-in">
        <div
          class="inline-flex items-center space-x-3 text-blue-300 text-sm bg-white/5 backdrop-blur-sm px-6 py-3 rounded-full border border-white/10"
        >
          <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M13 10V3L4 14h7v7l9-11h-7z"
            />
          </svg>
          <span class="font-bold">IntelliJob</span>
          <span class="text-slate-500">•</span>
          <span>© 2024</span>
        </div>
      </div>
    </div>

    <JobDetailModal v-if="isModalOpen" :job="selectedJob" @close="closeModal" />
  </div>
</template>

<style scoped>
/* Grid Pattern */
.bg-grid-pattern {
  background-image: linear-gradient(rgba(59, 130, 246, 0.1) 1px, transparent 1px),
    linear-gradient(90deg, rgba(59, 130, 246, 0.1) 1px, transparent 1px);
  background-size: 50px 50px;
}

/* Animations */
@keyframes fade-in-down {
  from {
    opacity: 0;
    transform: translateY(-30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
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

@keyframes fade-in {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes pulse-slow {
  0%,
  100% {
    opacity: 0.3;
  }
  50% {
    opacity: 0.6;
  }
}

@keyframes spin-slow {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

@keyframes gradient {
  0%,
  100% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
}

/* Apply Animations */
.animate-fade-in-down {
  animation: fade-in-down 0.8s ease-out;
}

.animate-fade-in-up {
  animation: fade-in-up 0.6s ease-out;
}

.animate-fade-in {
  animation: fade-in 0.5s ease-out;
}

.animate-pulse-slow {
  animation: pulse-slow 4s ease-in-out infinite;
}

.animate-spin-slow {
  animation: spin-slow 10s linear infinite;
}

.animate-gradient {
  background-size: 200% 200%;
  animation: gradient 3s ease infinite;
}

/* Animation Delays */
.animation-delay-200ms {
  animation-delay: 0.2s;
}

.animation-delay-400ms {
  animation-delay: 0.4s;
}

.animation-delay-2s {
  animation-delay: 2s;
}

.animation-delay-4s {
  animation-delay: 4s;
}

/* Floating Particles */
.particle {
  position: absolute;
  background: radial-gradient(circle, rgba(99, 102, 241, 0.3), transparent);
  border-radius: 50%;
  pointer-events: none;
  animation: float 6s ease-in-out infinite;
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

/* Components */
.badge-tech {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  background: rgba(59, 130, 246, 0.1);
  border: 1px solid rgba(59, 130, 246, 0.3);
  border-radius: 9999px;
  color: rgb(191, 219, 254);
  font-weight: 600;
  font-size: 0.875rem;
  backdrop-filter: blur(10px);
  animation: fade-in-up 0.6s ease-out;
}

/* Glass Effect */
.glass-card {
  background: rgba(15, 23, 42, 0.7);
  backdrop-filter: blur(20px);
}

/* Responsive */
@media (max-width: 640px) {
  .particle {
    display: none;
  }
}
</style>