<template>
  <section class="relative py-28 bg-green-50 overflow-hidden">
    <div class="absolute top-0 left-1/2 -translate-x-1/2 w-[500px] h-[200px] bg-primary/5 rounded-full blur-[70px] pointer-events-none"></div>
    <div class="relative max-w-3xl mx-auto px-6">
      <div class="text-center mb-16 reveal-up faq-header">
        <span class="faq-item text-xs font-bold tracking-[0.2em] text-primary uppercase">FAQ</span>
        <h2 class="faq-item text-4xl font-black text-gray-900 mt-4 mb-3">Common questions</h2>
        <p class="faq-item text-gray-500 text-sm">Everything you need to know before joining.</p>
      </div>
      <div class="space-y-3">
        <div v-for="(faq, i) in faqs" :key="faq.q" class="faq-card bg-white border border-green-100 rounded-2xl overflow-hidden hover:border-primary/25 hover:shadow-md hover:shadow-primary/5 transition-all duration-300" :style="`--card-delay:${0.42 + i * 0.09}s`">
          <button @click="toggle(i)" class="faq-card-item w-full flex items-center justify-between px-6 py-5 text-left group">
            <span class="font-bold text-gray-800 text-sm group-hover:text-primary transition-colors duration-300">{{ faq.q }}</span>
            <i class="fas text-gray-400 text-xs transition-all duration-300 shrink-0 ml-4" :class="open === i ? 'fa-minus text-primary' : 'fa-plus'"></i>
          </button>
          <transition enter-active-class="transition-all duration-300 ease-out" enter-from-class="opacity-0 max-h-0" enter-to-class="opacity-100 max-h-48" leave-active-class="transition-all duration-200 ease-in" leave-from-class="opacity-100 max-h-48" leave-to-class="opacity-0 max-h-0">
            <div v-if="open === i" class="px-6 pb-5 border-t border-green-100">
              <p class="text-sm text-gray-500 leading-relaxed pt-4">{{ faq.a }}</p>
            </div>
          </transition>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'FaqSection',
  data() { return { open: null, faqs: [
    { q: 'Who can register on this platform?', a: 'Any member of the CPCT Youth Wing of the Peaceful Struggle Movement can register. If you are a young person who supports justice and peace in Tigray, you are welcome.' },
    { q: 'Is my personal data safe?', a: 'Yes. All data is encrypted and protected by role-based access controls. Your information is only visible to verified coordinators and never shared externally without your consent.' },
    { q: 'Do I need technical experience to use it?', a: 'Not at all. The platform is designed to be simple and intuitive, even for members with no technical background. A Tigrinya interface is also available.' },
    { q: 'How will I be contacted after registering?', a: 'Once your profile is activated, you may be reached through the platform when there is an opportunity that matches your skills or availability.' },
    { q: 'Can I update my profile after registering?', a: 'Yes. You can log in at any time to update your skills, location, availability, or any other information.' },
    { q: 'Is there a cost to join?', a: 'No. Registration and use of the CPCT-Youth platform is completely free for all members.' },
  ] }; },
  methods: { toggle(i) { this.open = this.open === i ? null : i; } },
};
</script>

<style scoped>
.faq-item, .faq-card-item { opacity: 0; transform: translateY(28px); transition: opacity .7s cubic-bezier(.16,1,.3,1), transform .7s cubic-bezier(.16,1,.3,1); }
:global(.landing-section.revealed) .faq-item { opacity: 1; transform: translateY(0); }
:global(.landing-section.revealed) .faq-header .faq-item:nth-child(1) { transition-delay: .08s; }
:global(.landing-section.revealed) .faq-header .faq-item:nth-child(2) { transition-delay: .20s; }
:global(.landing-section.revealed) .faq-header .faq-item:nth-child(3) { transition-delay: .32s; }
:global(.landing-section.revealed) .faq-card .faq-card-item { opacity: 1; transform: translateY(0); transition-delay: var(--card-delay); }
@media (prefers-reduced-motion: reduce) { .faq-item, .faq-card-item { opacity: 1; transform: none; transition: none; } }
</style>
