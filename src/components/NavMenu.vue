<template>
<div class="nav-menu">
  <div class="container">
    <div class="nav-items">
      <div
        v-for="item in ['mens', 'womens', 'accessories', 'checkout']"
        :key="item"
        class="nav-item"
        :class="{ active: name === item, [item]: true }"
        @click="$router.push({ name: item })"
      >
        {{ $t(`demo.${item}.label`) }}
      </div>
      <div class="nav-underline" :style="underlineStyle" />
    </div>
    <div class="nav-search">
      <img :src="IcSearch">
    </div>
  </div>
</div>
</template>

<script>
import { computed } from 'vue';
import { useRoute } from 'vue-router';

export default {
  name: 'nav-menu',
  setup() {
    const route = useRoute();
    
    const underlineStyle = computed(() => {
      if(route.name === 'mens') {
        return { left: '-1px', width: '44px' };
      }
      if(route.name === 'womens') {
        return { left: '67px', width: '72px' };
      }
      if(route.name ==='accessories') {
        return { left: '161px', width: '104px' };
      }
      return { left: '289px', width: '82px' };
    });
    return {
      underlineStyle,
      name: route.name,
    };
  },
};
</script>

<style lang="postcss">
@import '../assets/css/global.css';

.nav-menu {
  background-color: white;
  .container {
    display: flex;
    height: 60px;
    justify-content: center;
    position: relative;
  }
  .nav-item, .nav-search {
    cursor: pointer;
  }
  .nav-items {
    @mixin title 14px;
    display: flex;
    align-items: center;
    color: $text-dark;
    line-height: 18px;
    position: relative;
    .nav-item:not(:last-child) {
      margin-right: 24px;
      cursor: pointer;
    }
    .nav-underline {
      position: absolute;
      bottom: 17px;
      height: 2px;
      background-color: black;
      transition-property: left width;
      transition-timing-function: ease-in;
      transition-duration: 0.3s;
    }
  }
  .nav-search {
    display: flex;
    align-items: center;
    position: absolute;
    right: 40px;
    height: 100%;
    width: 40px;
    img {
      height: 20px;
    }
  }
  @media (max-width: 568px) {
    .nav-search {
      display: none;
    }
    .checkout {
      display: none;
    }
  }
}
</style>
