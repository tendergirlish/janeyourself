<template>
  <ul class="nav justify-content-center my-3">
    <li v-for="btn in buttons" :key="btn.id" class="nav-item">
      <button
        class="btn btn-outline-secondary"
        :class="{ active: btn.id === activeSection }"
        @click="scrollToSection(btn.id)"
      >
        {{ btn.title }}
      </button>
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      buttons: [
        { id: 'intro', title: 'INTRO' },
        { id: 'about', title: 'ABOUT ME' },
        { id: 'project', title: 'PROJECT' },
        { id: 'portfolio', title: 'PORTFOLIO' },
        { id: 'contact', title: 'CONTACT' },
      ],
      activeSection: 'intro',
    };
  },
  methods: {
    scrollToSection(id) {
      document.getElementById(id).scrollIntoView({ behavior: 'smooth' });
      this.activeSection = id;
    },
  },
};
</script>
