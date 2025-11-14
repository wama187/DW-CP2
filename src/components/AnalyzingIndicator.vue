<template>
  <div class="mt-12 animate-fade-in">
    <div class="relative">
      <div
        class="absolute inset-0 bg-gradient-to-r from-blue-800 via-blue-600 to-blue-400 rounded-3xl blur-2xl opacity-20 animate-pulse"
      ></div>
      <div class="relative glass-card rounded-3xl p-12 border border-white/10">
        <div class="flex flex-col items-center space-y-6">
          <!-- Animated Loader -->
          <div class="relative w-32 h-32">
            <div class="absolute inset-0 border-8 border-slate-700 rounded-full"></div>
            <div class="absolute inset-0 border-8 border-blue-800 border-t-transparent rounded-full animate-spin"></div>
            <div
              class="absolute inset-4 border-8 border-blue-600 border-t-transparent rounded-full animate-spin-reverse"
            ></div>
            <div
              class="absolute inset-8 border-8 border-blue-400 border-t-transparent rounded-full animate-spin animation-delay-300ms"
            ></div>
          </div>

          <div class="text-center">
            <h3 class="text-3xl font-bold text-white mb-3 animate-pulse">Analizando tu CV con IA</h3>
            <p class="text-indigo-300 text-lg mb-6">Extrayendo habilidades, experiencia y educación...</p>

            <!-- Progress Steps -->
            <div class="flex flex-col sm:flex-row justify-center gap-4 mt-8">
              <div class="step-badge">
                <div class="step-icon">1</div>
                <span class="text-white">Procesando texto</span>
              </div>
              <div class="step-badge animation-delay-500ms">
                <div class="step-icon">2</div>
                <span class="text-white">Extrayendo habilidades</span>
              </div>
              <div class="step-badge animation-delay-1s">
                <div class="step-icon">3</div>
                <span class="text-white">Buscando matches</span>
              </div>
            </div>
          </div>

          <!-- Animated Dots -->
          <div class="flex space-x-3">
            <div class="w-4 h-4 bg-blue-800 rounded-full animate-bounce"></div>
            <div class="w-4 h-4 bg-blue-600 rounded-full animate-bounce animation-delay-200ms"></div>
            <div class="w-4 h-4 bg-blue-400 rounded-full animate-bounce animation-delay-400ms"></div>
          </div>
        </div>
      </div>
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
@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
.animate-spin {
  animation: spin 1s linear infinite;
}
@keyframes spin-reverse {
  from {
    transform: rotate(360deg);
  }
  to {
    transform: rotate(0deg);
  }
}
.animate-spin-reverse {
  animation: spin-reverse 1.5s linear infinite;
}
@keyframes bounce {
  0%,
  100% {
    transform: translateY(0);
    animation-timing-function: cubic-bezier(0.8, 0, 1, 1);
  }
  50% {
    transform: translateY(-25%);
    animation-timing-function: cubic-bezier(0, 0, 0.2, 1);
  }
}
.animate-bounce {
  animation: bounce 1s infinite;
}
.animation-delay-200ms {
  animation-delay: 0.2s;
}
.animation-delay-300ms {
  animation-delay: 0.3s;
}
.animation-delay-400ms {
  animation-delay: 0.4s;
}
.animation-delay-500ms {
  animation-delay: 0.5s;
}
.animation-delay-1s {
  animation-delay: 1s;
}
.step-badge {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem 1.5rem;
  background: rgba(59, 130, 246, 0.1);
  border: 1px solid rgba(59, 130, 246, 0.3);
  border-radius: 1rem;
  backdrop-filter: blur(10px);
  animation: fade-in 0.8s ease-out;
}

.step-icon {
  width: 2rem;
  height: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #1e40af, #3b82f6);
  color: white;
  font-weight: bold;
  border-radius: 0.5rem;
}
</style>
