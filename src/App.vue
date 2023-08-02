<script setup>
import DesHead from './components/DesHead.vue';
import HeaderView from './components/HeaderView.vue';
import NavLinks from './components/NavLinks.vue';
import MainView from './components/MainView.vue';
</script>

<template>
  <div class="">
    <HeaderView />
    <DesHead />
    <NavLinks />
    <main>
      <MainView />
    </main>
  </div>
</template>

<!-- <style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style> -->
