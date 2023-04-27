<template>
  <div class="menu">
    <Logo />
    <!-- Использование компонента Logo -->
    <MenuItem
      v-for="item in items"
      :key="item.id"
      :title="item.title"
      :link="item.link"
    />
    <!-- Использование компонента MenuItem -->
  </div>
</template>

<script>
import Logo from "./Logo.vue"; // Импорт компонента Logo
import MenuItem from "./MenuItem.vue"; // Импорт компонента MenuItem

export default {
  components: {
    Logo, // Регистрация компонента Logo в качестве дочернего компонента
    MenuItem, // Регистрация компонента MenuItem в качестве дочернего компонента
  },
  data() {
    return {
      items: [
        { id: 1, title: "Home", link: "/" },
        { id: 2, title: "About", link: "/about" },
        { id: 3, title: "Contact", link: "/contact" },
      ],
    };
  },
};
</script>

<style scoped>
.menu {
background-image: radial-gradient(circle at 29% 0, #000, #1c2734 103%);
  max-width: 229px;
  height: 100vh;
  /* Устанавливаем ширину компонента Menu.vue на 100% экрана */
  width: 100%;
  /* Устанавливаем отступы слева и справа на 0, чтобы компонент был прижат к левому краю экрана */
  margin-left: 0;
  padding: 0 55px 0 25px;  
  margin-right: 0;
}
</style>