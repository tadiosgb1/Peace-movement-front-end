<template>
  <section class="relative py-28 bg-green-50 overflow-hidden">
    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2
                w-[600px] h-[300px] bg-primary/8 rounded-full blur-[90px] pointer-events-none"></div>
    <div class="relative max-w-3xl mx-auto px-6 text-center reveal-up">
      <span class="inline-block px-4 py-1.5 mb-8 text-xs font-semibold tracking-widest
                   text-primary bg-primary/10 rounded-full uppercase border border-primary/20">
        <i class="fas fa-dove mr-2 animate-float"></i>Join the Movement Today
      </span>
      <h2 class="text-4xl lg:text-5xl font-black text-gray-900 mb-6 leading-[1.08]">
        Your talent deserves<br/>to make a difference.
      </h2>
      <p class="text-gray-500 mb-12 text-sm leading-relaxed max-w-xl mx-auto">
        Register your profile today and become a connected, recognized part of the CPCT Youth Wing —
        ready to contribute wherever you are needed most.
      </p>
      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <button @click="$emit('open-register')"
          class="group px-9 py-4 bg-primary hover:bg-primary-dark text-white font-bold rounded-2xl
                 shadow-xl shadow-primary/25 hover:shadow-primary/40 hover:-translate-y-1
                 transition-all duration-300 text-sm flex items-center justify-center gap-3">
          Register — It's Free
          <i class="fas fa-arrow-right text-xs group-hover:translate-x-1.5 transition-transform duration-300"></i>
        </button>
        <button @click="$emit('open-login')"
          class="px-9 py-4 bg-white text-gray-700 font-semibold rounded-2xl border border-green-200
                 hover:border-primary/40 hover:text-primary transition-all duration-300 text-sm shadow-sm">
          Sign In
        </button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'CtaSection',
  emits: ['open-register', 'open-login'],
};
</script>

<style scoped>
@keyframes float {
  0%, 100% { transform: translateY(0); }
  50%       { transform: translateY(-5px); }
}
.animate-float { animation: float 3s ease-in-out infinite; }
</style>
