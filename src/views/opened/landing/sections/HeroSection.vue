<template>
  <section class="relative bg-slate-900 py-20 overflow-hidden">
    <!-- Glow blobs -->
    <div class="absolute inset-0 opacity-[0.12] pointer-events-none">
      <div class="absolute top-0 right-0 w-[500px] h-[500px] bg-primary rounded-full blur-3xl"></div>
      <div class="absolute bottom-0 left-0 w-[400px] h-[400px] bg-secondary rounded-full blur-3xl"></div>
      <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[300px] bg-tertiary-light rounded-full blur-[100px]"></div>
    </div>
    <!-- Dot grid -->
    <div class="absolute inset-0 opacity-[0.04] pointer-events-none"
      style="background-image:radial-gradient(circle,#fff 1px,transparent 1px);background-size:32px 32px">
    </div>

    <div class="relative z-10 max-w-4xl mx-auto px-6 text-center hero-text">
      <!-- Badge -->
      <span class="inline-block px-4 py-1.5 mb-8 text-xs font-semibold tracking-widest
                   text-primary-light bg-primary/10 rounded-full uppercase border border-primary/20">
        <i class="fas fa-dove mr-2 animate-float"></i>CPCT Youth Wing · Peaceful Struggle Movement
      </span>

      <!-- Headline -->
      <h1 class="text-4xl sm:text-5xl lg:text-6xl font-black text-white leading-tight mb-6 tracking-tight">
        Unite Your Skills.<br/>
        <span class="text-primary-light">Strengthen the Movement.</span>
      </h1>

      <!-- Sub-headline -->
      <p class="text-slate-400 text-lg leading-relaxed max-w-2xl mx-auto mb-10">
        A secure digital home for the youth of Tigray — where your profession, skills, and aspirations
        are recognized, connected, and mobilized for justice and lasting peace.
      </p>

      <!-- CTAs -->
      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <button @click="$emit('open-register')"
          class="group px-9 py-4 bg-primary hover:bg-primary-dark text-white font-bold rounded-2xl
                 shadow-xl shadow-primary/30 hover:shadow-primary/50
                 hover:-translate-y-1 transition-all duration-300 text-sm
                 flex items-center justify-center gap-3">
          Register Your Profile — Free
          <i class="fas fa-arrow-right text-xs group-hover:translate-x-1.5 transition-transform duration-300"></i>
        </button>
        <a href="#about"
          class="px-9 py-4 bg-white/5 hover:bg-white/10 text-white font-semibold rounded-2xl
                 border border-white/10 hover:border-primary/40
                 transition-all duration-300 text-sm flex items-center justify-center gap-2">
          <i class="fas fa-info-circle text-primary-light text-xs"></i>
          Learn More
        </a>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'HeroSection',
  emits: ['open-register'],
};
</script>

<style scoped>
.hero-text {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.85s cubic-bezier(0.16,1,0.3,1), transform 0.85s cubic-bezier(0.16,1,0.3,1);
}
.hero-text.revealed { opacity: 1; transform: translateY(0); }

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50%       { transform: translateY(-5px); }
}
.animate-float { animation: float 3s ease-in-out infinite; }
</style>
