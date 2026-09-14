<template>
  <section id="about" class="relative py-28 bg-white overflow-hidden scroll-mt-24">
    <div class="absolute top-0 right-0 w-[450px] h-[450px] bg-primary/5 rounded-full blur-[100px] pointer-events-none"></div>
    <div class="absolute bottom-0 left-0 w-[350px] h-[350px] bg-secondary/4 rounded-full blur-[80px] pointer-events-none"></div>
    <div class="relative max-w-7xl mx-auto px-6">
      <div class="flex flex-col lg:flex-row items-center gap-16">
        <div class="flex-1 reveal-left">
          <div class="relative grid grid-cols-2 gap-4">
            <div v-for="(card, i) in cards" :key="card.title"
              class="about-item group bg-white border border-green-100 rounded-2xl p-6 hover:border-primary/30 hover:shadow-xl hover:shadow-primary/6 hover:-translate-y-1 transition-all duration-300"
              :style="`--item-delay:${i * 0.12}s`">
              <div class="w-10 h-10 rounded-xl flex items-center justify-center mb-4 group-hover:scale-110 transition-transform duration-300" :class="card.bg">
                <i :class="[card.icon, card.color, 'text-sm']"></i>
              </div>
              <p class="font-black text-gray-800 text-sm mb-1">{{ card.title }}</p>
              <p class="text-xs text-gray-500 leading-relaxed">{{ card.desc }}</p>
            </div>
            <div class="absolute -bottom-10 -left-10 w-52 h-52 bg-primary-lighter rounded-full blur-3xl -z-10 opacity-60"></div>
          </div>
        </div>

        <div class="flex-1 reveal-right about-copy">
          <span class="about-item text-xs font-bold tracking-[0.2em] text-primary uppercase">About the Platform</span>
          <h2 class="about-item text-4xl font-black text-gray-900 mt-4 mb-6 leading-tight">Your skills matter.<br/>Your voice is needed.</h2>
          <p class="about-item text-gray-500 text-sm leading-relaxed mb-5">The CPCT-Youth Online Platform is a secure, easy-to-use space where members of the Youth Wing can register their profession, skills, location, and availability — making it possible for coordinators to connect the right person to the right opportunity at the right time.</p>
          <p class="about-item text-gray-500 text-sm leading-relaxed mb-8">Whether you are a lawyer, teacher, engineer, student, or communicator — your contribution has a place in the peaceful struggle for justice in Tigray.</p>
          <router-link to="/about" class="about-item group inline-flex items-center gap-3 px-6 py-3 bg-primary hover:bg-primary-dark text-white font-bold rounded-xl shadow-lg shadow-primary/20 hover:-translate-y-0.5 transition-all duration-300 text-sm">
            Learn More About CPCT
            <i class="fas fa-arrow-right text-xs group-hover:translate-x-1 transition-transform duration-300"></i>
          </router-link>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'AboutSection',
  data() {
    return { cards: [
      { title: 'Know Your Members', desc: 'Every profile searchable by skill, profession, and location.', icon: 'fas fa-id-badge', bg: 'bg-primary-lighter', color: 'text-primary' },
      { title: 'Fast Mobilization', desc: 'Coordinators find the right people in minutes, not days.', icon: 'fas fa-bolt', bg: 'bg-secondary-lighter', color: 'text-secondary' },
      { title: 'Skills-Based Match', desc: 'Tasks matched to members based on real expertise and availability.', icon: 'fas fa-puzzle-piece', bg: 'bg-tertiary-lighter', color: 'text-tertiary' },
      { title: 'Privacy First', desc: 'Encrypted data, shared only with authorized coordinators.', icon: 'fas fa-shield-alt', bg: 'bg-primary-lighter', color: 'text-primary' },
    ] };
  },
};
</script>

<style scoped>
.about-item { opacity: 0; transform: translateY(28px); transition: opacity 0.7s cubic-bezier(0.16,1,0.3,1), transform 0.7s cubic-bezier(0.16,1,0.3,1); transition-delay: var(--item-delay, 0s); }
:global(.landing-section.revealed) .about-item { opacity: 1; transform: translateY(0); }
.about-copy .about-item:nth-child(1) { --item-delay: 0.10s; }
.about-copy .about-item:nth-child(2) { --item-delay: 0.22s; }
.about-copy .about-item:nth-child(3) { --item-delay: 0.34s; }
.about-copy .about-item:nth-child(4) { --item-delay: 0.46s; }
.about-copy .about-item:nth-child(5) { --item-delay: 0.58s; }
@media (prefers-reduced-motion: reduce) { .about-item { opacity: 1; transform: none; transition: none; } }
</style>
