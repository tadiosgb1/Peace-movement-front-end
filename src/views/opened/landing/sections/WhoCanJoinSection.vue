<template>
  <section class="relative py-28 bg-white overflow-hidden">
    <div class="absolute bottom-0 right-0 w-[400px] h-[400px] bg-secondary/5 rounded-full blur-[100px] pointer-events-none"></div>
    <div class="absolute top-0 left-0 w-[300px] h-[300px] bg-primary/4 rounded-full blur-[80px] pointer-events-none"></div>
    <div class="relative max-w-7xl mx-auto px-6">
      <div class="text-center mb-16 reveal-up join-header">
        <span class="join-item text-xs font-bold tracking-[0.2em] text-primary uppercase">Who Can Join</span>
        <h2 class="join-item text-4xl font-black text-gray-900 mt-4 mb-4">A home for every young voice</h2>
        <p class="join-item text-gray-500 max-w-lg mx-auto text-sm leading-relaxed">No matter your background — if you believe in a peaceful and just Tigray, there is a role for you.</p>
      </div>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-5">
        <div v-for="(aud, i) in audiences" :key="aud.title" class="join-card group relative bg-white border border-green-100 rounded-2xl p-6 hover:border-primary/30 hover:shadow-xl hover:shadow-primary/8 hover:-translate-y-2 transition-all duration-300 overflow-hidden" :style="`--card-delay:${0.42 + i * 0.13}s`">
          <div class="absolute top-0 left-0 right-0 h-[3px] rounded-t-2xl bg-primary scale-x-0 group-hover:scale-x-100 origin-left transition-transform duration-300"></div>
          <div class="join-card-item w-12 h-12 rounded-xl bg-green-50 flex items-center justify-center mb-5 group-hover:scale-110 transition-transform duration-300">
            <i :class="[aud.icon, 'text-primary text-lg']"></i>
          </div>
          <h3 class="join-card-item font-black text-gray-800 text-sm mb-2 group-hover:text-primary transition-colors duration-300">{{ aud.title }}</h3>
          <p class="join-card-item text-xs text-gray-500 leading-relaxed">{{ aud.desc }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'WhoCanJoinSection',
  data() { return { audiences: [
    { title: 'Professionals', desc: 'Lawyers, doctors, engineers, teachers, and researchers contributing their expertise to the cause.', icon: 'fas fa-briefcase' },
    { title: 'Students & Youth', desc: 'University students and graduates eager to make a meaningful impact in their region.', icon: 'fas fa-user-graduate' },
    { title: 'Communicators', desc: 'Journalists, advocates, and content creators amplifying the voice of the peaceful movement.', icon: 'fas fa-bullhorn' },
    { title: 'Community Leaders', desc: 'Local organizers and representatives bridging the movement to every corner of Tigray.', icon: 'fas fa-people-carry' },
  ] }; },
};
</script>

<style scoped>
.join-item, .join-card-item { opacity: 0; transform: translateY(28px); transition: opacity .7s cubic-bezier(.16,1,.3,1), transform .7s cubic-bezier(.16,1,.3,1); }
:global(.landing-section.revealed) .join-item { opacity: 1; transform: translateY(0); }
:global(.landing-section.revealed) .join-header .join-item:nth-child(1) { transition-delay: .08s; }
:global(.landing-section.revealed) .join-header .join-item:nth-child(2) { transition-delay: .20s; }
:global(.landing-section.revealed) .join-header .join-item:nth-child(3) { transition-delay: .32s; }
:global(.landing-section.revealed) .join-card .join-card-item { opacity: 1; transform: translateY(0); transition-delay: var(--card-delay); }
@media (prefers-reduced-motion: reduce) { .join-item, .join-card-item { opacity: 1; transform: none; transition: none; } }
</style>
