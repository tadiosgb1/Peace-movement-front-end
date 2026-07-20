<template>
  <div class="min-h-screen bg-white font-sans text-gray-800 ">
    <Header @open-login="showLogin = true" @open-register="showRegister = true" />

    <!-- ══════════════════════════════════════════════════════════
         HERO
    ══════════════════════════════════════════════════════════ -->
    <section class="relative bg-slate-900 py-24 overflow-hidden">
      <div class="absolute inset-0 opacity-[0.12] pointer-events-none">
        <div class="absolute top-0 right-0 w-96 h-96 bg-primary rounded-full blur-3xl"></div>
        <div class="absolute bottom-0 left-0 w-72 h-72 bg-secondary rounded-full blur-3xl"></div>
      </div>
      <div class="absolute inset-0 opacity-[0.04] pointer-events-none"
        style="background-image:radial-gradient(circle,#fff 1px,transparent 1px);background-size:32px 32px">
      </div>
      <div class="relative max-w-4xl mx-auto px-6 text-center">
        <span class="inline-block px-4 py-1.5 mb-6 text-xs font-semibold tracking-widest
                     text-primary-light bg-primary/10 rounded-full uppercase border border-primary/20">
          <i class="fas fa-newspaper mr-2"></i>News &amp; Events
        </span>
        <h1 class="text-4xl sm:text-5xl font-black text-white leading-tight mb-6">
          Stay Connected<br/>
          <span class="text-primary-light">to the Movement</span>
        </h1>
        <p class="text-slate-400 text-lg leading-relaxed max-w-2xl mx-auto">
          Platform updates, coordination announcements, upcoming events, and stories from
          the youth of Tigray working for peaceful change.
        </p>
      </div>
    </section>

    <!-- ══════════════════════════════════════════════════════════
         POSTS GRID  — loaded from server
    ══════════════════════════════════════════════════════════ -->
    <section class="py-16 bg-white">
      <div class="max-w-7xl mx-auto px-6">

        <!-- Loading state -->
        <div v-if="loading" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
          <div v-for="n in 6" :key="n"
            class="rounded-2xl border border-green-100 overflow-hidden animate-pulse">
            <div class="h-44 bg-green-50"></div>
            <div class="p-6 space-y-3">
              <div class="h-3 bg-gray-100 rounded-full w-1/3"></div>
              <div class="h-4 bg-gray-100 rounded-full w-full"></div>
              <div class="h-4 bg-gray-100 rounded-full w-4/5"></div>
              <div class="h-3 bg-gray-100 rounded-full w-2/3"></div>
            </div>
          </div>
        </div>

        <!-- Posts grid -->
        <div v-else-if="filteredPosts.length > 0"
          class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
          <article
            v-for="post in filteredPosts" :key="post.id"
            class="bg-white rounded-2xl border border-green-100
                   hover:border-primary/30 hover:shadow-lg hover:-translate-y-1
                   transition-all duration-300 group flex flex-col overflow-hidden">
            <!-- Thumbnail -->
            <div class="h-44 bg-green-50 flex items-center justify-center overflow-hidden relative">
              <img v-if="post.image" :src="post.image" :alt="post.title"
                class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300" />
              <i v-else class="fas fa-newspaper text-4xl text-primary/30"></i>
              <span v-if="post.tag"
                class="absolute top-4 left-4 px-3 py-1 text-[9px] font-black rounded-full uppercase
                       tracking-widest bg-primary-lighter text-primary border border-primary/20">
                {{ post.tag }}
              </span>
            </div>
            <!-- Body -->
            <div class="p-6 flex flex-col flex-1">
              <p class="text-[10px] text-gray-400 font-bold uppercase tracking-widest mb-2">{{ post.date }}</p>
              <h3 class="font-black text-gray-800 text-base leading-snug mb-3
                         group-hover:text-primary transition-colors duration-300">
                {{ post.title }}
              </h3>
              <p class="text-xs text-gray-500 leading-relaxed flex-1">{{ post.excerpt }}</p>
              <a :href="post.url || '#'"
                class="mt-5 inline-flex items-center gap-1.5 text-primary hover:text-primary-dark
                       text-xs font-bold transition-colors">
                Read More <i class="fas fa-arrow-right text-[10px]"></i>
              </a>
            </div>
          </article>
        </div>

        <!-- Empty state -->
        <div v-else class="text-center py-32">
          <div class="w-16 h-16 bg-green-50 rounded-2xl flex items-center justify-center mx-auto mb-5">
            <i class="fas fa-newspaper text-2xl text-primary/40"></i>
          </div>
          <p class="text-gray-400 font-semibold text-sm">No posts available yet. Check back soon.</p>
        </div>

        <!-- Pagination -->
        <div v-if="totalPages > 1" class="mt-14 flex items-center justify-center gap-2">
          <button @click="prevPage" :disabled="currentPage === 1"
            class="w-10 h-10 rounded-xl bg-green-50 border border-green-100 flex items-center justify-center
                   text-primary disabled:opacity-40 hover:bg-primary hover:text-white
                   hover:border-primary transition-all duration-200">
            <i class="fas fa-chevron-left text-xs"></i>
          </button>
          <span class="px-5 py-2 text-sm font-bold text-gray-600">
            Page {{ currentPage }} of {{ totalPages }}
          </span>
          <button @click="nextPage" :disabled="currentPage === totalPages"
            class="w-10 h-10 rounded-xl bg-green-50 border border-green-100 flex items-center justify-center
                   text-primary disabled:opacity-40 hover:bg-primary hover:text-white
                   hover:border-primary transition-all duration-200">
            <i class="fas fa-chevron-right text-xs"></i>
          </button>
        </div>
      </div>
    </section>

    <Footer />

    <login-modal    v-if="showLogin"    @close="showLogin = false"    @switch-to-register="showLogin = false; showRegister = true" />
    <register-modal v-if="showRegister" @close="showRegister = false" @switch-to-login="showRegister = false; showLogin = true" />
  </div>
</template>

<script>
import Header        from './header.vue';
import Footer        from './footer.vue';
import LoginModal    from '@/components/AuthModal.vue';
import RegisterModal from '@/components/RegisterModal.vue';

export default {
  name: 'NewsEventsPage',
  components: { Header, Footer, LoginModal, RegisterModal },

  data() {
    return {
      showLogin:    false,
      showRegister: false,
      loading:      true,
      posts:        [],
      currentPage:  1,
      totalPages:   1,
      perPage:      9,
    };
  },

  computed: {
    filteredPosts() {
      return this.posts;
    },
  },

  watch: {},

  methods: {
    async fetchPosts() {
      this.loading = true;
      try {
        const params = new URLSearchParams({
          page:     this.currentPage,
          per_page: this.perPage,
        });
        const data = await this.$apiGet(`/news?${params}`);
        this.posts      = data.posts      ?? [];
        this.totalPages = data.totalPages ?? 1;
      } catch {
        this.posts = [];
      } finally {
        this.loading = false;
      }
    },

    prevPage() {
      if (this.currentPage > 1) { this.currentPage--; this.fetchPosts(); }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) { this.currentPage++; this.fetchPosts(); }
    },
  },

  mounted() {
    this.fetchPosts();
  },
};
</script>
