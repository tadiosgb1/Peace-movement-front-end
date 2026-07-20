<template>
  <section class="relative py-28 bg-white overflow-hidden">
    <div class="absolute bottom-0 right-0 w-[400px] h-[400px] bg-secondary/5 rounded-full blur-[100px] pointer-events-none"></div>
    <div class="absolute top-0 left-0 w-[300px] h-[300px] bg-primary/4 rounded-full blur-[80px] pointer-events-none"></div>
    <div class="relative max-w-7xl mx-auto px-6">
      <div class="text-center mb-16 reveal-up">
        <span class="text-xs font-bold tracking-[0.2em] text-primary uppercase">Who Can Join</span>
        <h2 class="text-4xl font-black text-gray-900 mt-4 mb-4">A home for every young voice</h2>
        <p class="text-gray-500 max-w-lg mx-auto text-sm leading-relaxed">
          No matter your background — if you believe in a peaceful and just Tigray, there is a role for you.
        </p>
      </div>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-5">
        <div v-for="(aud, i) in audiences" :key="aud.title"
          class="reveal-up group relative bg-white border border-green-100 rounded-2xl p-6
                 hover:border-primary/30 hover:shadow-xl hover:shadow-primary/8
                 hover:-translate-y-2 transition-all duration-300 overflow-hidden"
          :style="`transition-delay:${i * 0.1}s`">
          <div class="absolute top-0 left-0 right-0 h-[3px] rounded-t-2xl bg-primary
                      scale-x-0 group-hover:scale-x-100 origin-left transition-transform duration-300"></div>
          <div class="w-12 h-12 rounded-xl bg-green-50 flex items-center justify-center mb-5
                      group-hover:scale-110 transition-transform duration-300">
            <i :class="[aud.icon, 'text-primary text-lg']"></i>
          </div>
          <h3 class="font-black text-gray-800 text-sm mb-2 group-hover:text-primary transition-colors duration-300">{{ aud.title }}</h3>
          <p class="text-xs text-gray-500 leading-relaxed">{{ aud.desc }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'WhoCanJoinSection',
  data() {
    return {
      audiences: [
        { title: 'Professionals',     desc: 'Lawyers, doctors, engineers, teachers, and researchers contributing their expertise to the cause.',  icon: 'fas fa-briefcase' },
        { title: 'Students & Youth',  desc: 'University students and graduates eager to make a meaningful impact in their region.',                icon: 'fas fa-user-graduate' },
        { title: 'Communicators',     desc: 'Journalists, advocates, and content creators amplifying the voice of the peaceful movement.',        icon: 'fas fa-bullhorn' },
        { title: 'Community Leaders', desc: 'Local organizers and representatives bridging the movement to every corner of Tigray.',              icon: 'fas fa-people-carry' },
      ],
    };
  },
};
</script>
