<template>
  <section :id="section.id" class="py-5 bg-light">
    <div class="container">
      <h2>{{ section.title }}</h2>
      <p>{{ section.content }}</p>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    section: Object,
  },
};
</script>
