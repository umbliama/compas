<template>
  <li class="menu-item">
      <a class="menu-item__link" :href="link">{{ title }}</a>
  </li>
</template>

<script>
export default {
    props:{
        title:{
            type:String,
            required:true,
        },
        link:{
            type:String,
            required:true,
        }
    }

}
// Ваш код скрипта для компонента MenuItem здесь
</script>

<style lang="scss" scoped>
/* Ваши стили для компонента MenuItem здесь */
.menu-item {
    list-style: none;
    &__link {
    }
}
</style>