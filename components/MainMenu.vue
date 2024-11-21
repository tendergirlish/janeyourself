<template>
  <nav class="navbar navbar-expand-lg text-light">
    <div class="container">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li v-for="item in menuItems" :key="item.id" class="nav-item">
          <nuxt-link class="nav-link" :to="`/${item.id}`">{{ item.title }}</nuxt-link>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'MainMenu',
  data() {
    return {
      menuItems: [
        { id: 'intro', title: 'INTRO' },
        { id: 'about', title: 'ABOUT ME' },
        { id: 'project', title: 'PROJECT' },
        { id: 'portfolio', title: 'PORTFOLIO' },
        { id: 'contact', title: 'CONTACT' },
      ],
    };
  },
};
</script>
