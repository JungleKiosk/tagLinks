<script>
import { RouterView, RouterLink, useRoute } from "vue-router";
import NavbarVue from "./components/partials/NavbarVue.vue";
import { ref, onMounted } from "vue";

export default {
  name: 'App',
  components: {
    NavbarVue
  },
  setup() {
    const route = useRoute();

    // Dark mode logic
    const isDarkMode = ref(true);

    const applyTheme = () => {
      document.body.classList.remove('dark_mode', 'light_mode');
      document.body.classList.add(isDarkMode.value ? 'dark_mode' : 'light_mode');
    };

    onMounted(() => {
      const savedTheme = localStorage.getItem('theme');
      if (savedTheme) {
        isDarkMode.value = savedTheme === 'dark';
      } else {
        localStorage.setItem('theme', 'dark');
      }
      applyTheme();
    });

    const toggleTheme = () => {
      isDarkMode.value = !isDarkMode.value;
      const theme = isDarkMode.value ? 'dark' : 'light';
      localStorage.setItem('theme', theme);
      applyTheme();
    };

    return { route, isDarkMode, toggleTheme };
  }
};
</script>

<template>
  <NavbarVue :isDarkMode="isDarkMode" :toggleTheme="toggleTheme" />

  <div class="content mt-5 pt-5">
    <router-view />
  </div>

</template>

<style></style>