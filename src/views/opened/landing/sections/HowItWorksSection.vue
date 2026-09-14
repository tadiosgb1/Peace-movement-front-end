<template>
  <section class="relative py-28 bg-green-50 overflow-hidden">
    <div class="absolute top-0 left-1/2 -translate-x-1/2 w-[600px] h-[250px] bg-primary/6 rounded-full blur-[80px] pointer-events-none"></div>
    <div class="relative max-w-7xl mx-auto px-6">
      <div class="text-center mb-20 reveal-up how-header">
        <span class="how-item text-xs font-bold tracking-[0.2em] text-primary uppercase">How It Works</span>
        <h2 class="how-item text-4xl font-black text-gray-900 mt-4 mb-4">Get involved in 3 simple steps</h2>
        <p class="how-item text-gray-500 max-w-lg mx-auto text-sm leading-relaxed">From sign-up to being matched with meaningful tasks — simple, fast, and fully secure.</p>
      </div>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 relative">
        <div class="hidden md:block absolute top-9 left-[calc(16.67%+48px)] right-[calc(16.67%+48px)] h-px bg-gradient-to-r from-transparent via-primary/30 to-transparent"></div>
        <div v-for="(step, i) in steps" :key="step.title" class="how-card text-center relative group" :style="`--card-delay:${0.42 + i * 0.16}s`">
          <div class="relative inline-flex mb-7 how-card-item">
            <div class="w-20 h-20 rounded-2xl flex items-center justify-center bg-white shadow-lg shadow-green-100 group-hover:shadow-primary/15 group-hover:scale-105 transition-all duration-300 border border-green-100">
              <i :class="[step.icon, 'text-primary text-2xl']"></i>
            </div>
            <span class="absolute -top-2.5 -right-2.5 w-6 h-6 rounded-full bg-primary text-white text-[10px] font-black flex items-center justify-center shadow-md">{{ i + 1 }}</span>
          </div>
          <h3 class="how-card-item font-black text-gray-800 text-base mb-2 group-hover:text-primary transition-colors duration-300">{{ step.title }}</h3>
          <p class="how-card-item text-sm text-gray-500 leading-relaxed max-w-xs mx-auto">{{ step.desc }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'HowItWorksSection',
  data() { return { steps: [
    { title: 'Create Your Profile', desc: 'Register your name, profession, skills, location, and availability in just a few minutes.', icon: 'fas fa-user-plus' },
    { title: 'Get Verified & Connected', desc: 'A coordinator reviews and activates your profile so you appear in search and matching results.', icon: 'fas fa-user-check' },
    { title: 'Contribute & Grow', desc: 'Get matched to campaigns, tasks, and opportunities that fit your unique skills and availability.', icon: 'fas fa-hands-helping' },
  ] }; },
};
</script>

<style scoped>
.how-item, .how-card-item { opacity: 0; transform: translateY(28px); transition: opacity .7s cubic-bezier(.16,1,.3,1), transform .7s cubic-bezier(.16,1,.3,1); }
:global(.landing-section.revealed) .how-item { opacity: 1; transform: translateY(0); }
:global(.landing-section.revealed) .how-header .how-item:nth-child(1) { transition-delay: .08s; }
:global(.landing-section.revealed) .how-header .how-item:nth-child(2) { transition-delay: .20s; }
:global(.landing-section.revealed) .how-header .how-item:nth-child(3) { transition-delay: .32s; }
:global(.landing-section.revealed) .how-card .how-card-item { opacity: 1; transform: translateY(0); transition-delay: var(--card-delay); }
@media (prefers-reduced-motion: reduce) { .how-item, .how-card-item { opacity: 1; transform: none; transition: none; } }
</style>
