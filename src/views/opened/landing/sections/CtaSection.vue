<template>
  <section class="relative py-28 bg-green-50 overflow-hidden">
    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[300px] bg-primary/8 rounded-full blur-[90px] pointer-events-none"></div>
    <div class="relative max-w-3xl mx-auto px-6 text-center reveal-up cta-content">
      <span class="cta-item inline-block px-4 py-1.5 mb-8 text-xs font-semibold tracking-widest text-primary bg-primary/10 rounded-full uppercase border border-primary/20">
        <i class="fas fa-dove mr-2 animate-float"></i>Join the Movement Today
      </span>
      <h2 class="cta-item text-4xl lg:text-5xl font-black text-gray-900 mb-6 leading-[1.08]">Your talent deserves<br/>to make a difference.</h2>
      <p class="cta-item text-gray-500 mb-12 text-sm leading-relaxed max-w-xl mx-auto">Register your profile today and become a connected, recognized part of the CPCT Youth Wing — ready to contribute wherever you are needed most.</p>
      <div class="cta-item flex flex-col sm:flex-row gap-4 justify-center">
        <button @click="$emit('open-register')" class="group px-9 py-4 bg-primary hover:bg-primary-dark text-white font-bold rounded-2xl shadow-xl shadow-primary/25 hover:shadow-primary/40 hover:-translate-y-1 transition-all duration-300 text-sm flex items-center justify-center gap-3">
          Register — It's Free
          <i class="fas fa-arrow-right text-xs group-hover:translate-x-1.5 transition-transform duration-300"></i>
        </button>
        <button @click="$emit('open-login')" class="px-9 py-4 bg-white text-gray-700 font-semibold rounded-2xl border border-green-200 hover:border-primary/40 hover:text-primary transition-all duration-300 text-sm shadow-sm">Sign In</button>
      </div>
    </div>
  </section>
</template>

<script>
export default { name: 'CtaSection', emits: ['open-register', 'open-login'] };
</script>

<style scoped>
.cta-item { opacity: 0; transform: translateY(28px); transition: opacity .7s cubic-bezier(.16,1,.3,1), transform .7s cubic-bezier(.16,1,.3,1); }
:global(.landing-section.revealed) .cta-item { opacity: 1; transform: translateY(0); }
:global(.landing-section.revealed) .cta-content .cta-item:nth-child(1) { transition-delay: .08s; }
:global(.landing-section.revealed) .cta-content .cta-item:nth-child(2) { transition-delay: .20s; }
:global(.landing-section.revealed) .cta-content .cta-item:nth-child(3) { transition-delay: .32s; }
:global(.landing-section.revealed) .cta-content .cta-item:nth-child(4) { transition-delay: .44s; }
@keyframes float { 0%,100% { transform: translateY(0); } 50% { transform: translateY(-5px); } }
.animate-float { animation: float 3s ease-in-out infinite; }
@media (prefers-reduced-motion: reduce) { .cta-item { opacity: 1; transform: none; transition: none; } }
</style>
