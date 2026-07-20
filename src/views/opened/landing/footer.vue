<template>
  <footer class="bg-primary-dark text-white pt-16 pb-8 px-6">
    <div class="max-w-7xl mx-auto">

      <!-- Top section -->
      <div class="grid grid-cols-1 md:grid-cols-5 gap-12 pb-12 border-b border-white/10">

        <!-- Brand column -->
        <div class="md:col-span-2 space-y-5">
          <div class="flex items-center gap-3">
            <div class="w-10 h-10 bg-primary-light rounded-xl flex items-center justify-center shadow-lg">
              <i class="fas fa-dove text-white text-base"></i>
            </div>
            <div>
              <span class="text-lg font-black text-white tracking-tight">
                CPCT<span class="text-tertiary-light">-Youth</span>
              </span>
              <p class="text-[10px] text-white/40 uppercase tracking-widest leading-none mt-0.5">
                Peaceful Struggle Movement
              </p>
            </div>
          </div>

          <p class="text-white/50 text-sm leading-relaxed max-w-sm">
            A digital platform for the youth wing of the Peaceful Struggle Movement — connecting skills, professions, and aspirations to advance justice and peace in Tigray.
          </p>

          <div class="flex items-start gap-2 text-xs text-white/40">
            <i class="fas fa-map-marker-alt mt-0.5 text-secondary-light"></i>
            <span>Addis Ababa, Ethiopia · July 2026</span>
          </div>

          <!-- Social links -->
          <div class="flex gap-3">
            <a v-for="social in socials" :key="social.name" href="#"
              :aria-label="social.name"
              class="w-9 h-9 rounded-xl bg-white/5 hover:bg-primary-light flex items-center justify-center transition-all duration-200 group">
              <i :class="[social.icon, 'text-sm text-white/50 group-hover:text-white transition-colors']"></i>
            </a>
          </div>
        </div>

        <!-- Nav columns -->
        <div v-for="group in navGroups" :key="group.title">
          <h3 class="text-[10px] font-bold uppercase tracking-[0.2em] text-white/30 mb-5">{{ group.title }}</h3>
          <ul class="space-y-3">
            <li v-for="link in group.links" :key="link.name">
              <router-link v-if="link.route" :to="link.route"
                class="text-sm text-white/60 hover:text-tertiary-light transition-colors">
                {{ link.name }}
              </router-link>
              <a v-else href="#"
                class="text-sm text-white/60 hover:text-tertiary-light transition-colors">
                {{ link.name }}
              </a>
            </li>
          </ul>
        </div>

      </div>

      <!-- Bottom bar -->
      <div class="pt-8 flex flex-col md:flex-row items-center justify-between gap-4">
        <p class="text-xs text-white/30">
          © {{ new Date().getFullYear() }} CPCT-Youth Wing — Peaceful Struggle Movement. All rights reserved.
        </p>
        <div class="flex gap-6">
          <a href="#" class="text-xs text-white/30 hover:text-white/60 transition-colors">Privacy Policy</a>
          <a href="#" class="text-xs text-white/30 hover:text-white/60 transition-colors">Terms of Use</a>
          <a href="#" class="text-xs text-white/30 hover:text-white/60 transition-colors">Data Consent</a>
        </div>
        <a href="#top"
          class="w-10 h-10 bg-white/5 hover:bg-primary-light border border-white/10 hover:border-primary-light rounded-xl flex items-center justify-center text-white/40 hover:text-white transition-all duration-300 hover:-translate-y-0.5"
          title="Back to top">
          <i class="fas fa-arrow-up text-xs"></i>
        </a>
      </div>

    </div>
  </footer>
</template>

<script>
export default {
  name: 'SiteFooter',
  data() {
    return {
      socials: [
        { name: 'Telegram', icon: 'fab fa-telegram-plane' },
        { name: 'Facebook', icon: 'fab fa-facebook-f' },
        { name: 'Twitter',  icon: 'fab fa-twitter' },
        { name: 'YouTube',  icon: 'fab fa-youtube' },
      ],
      navGroups: [
        {
          title: 'Platform',
          links: [
            { name: 'Youth Profiles',   route: null },
            { name: 'Skill Directory',  route: null },
            { name: 'Task Matching',    route: null },
            { name: 'Admin Dashboard',  route: null },
          ],
        },
        {
          title: 'Resources',
          links: [
            { name: 'TOR Document',     route: null },
            { name: 'User Guide',       route: null },
            { name: 'Tigrinya Support', route: null },
            { name: 'System Status',    route: null },
          ],
        },
        {
          title: 'Movement',
          links: [
            { name: 'About CPCT',       route: '/about' },
            { name: 'News & Updates',   route: '/news-events' },
            { name: 'Contact Us',       route: '/contact' },
            { name: 'Join the Movement',route: null },
          ],
        },
      ],
    };
  },
};
</script>
