<template>
<div class="header-wrap">
  <div class="header container">
    <div class="header-title">
      {{ $t('demo.title') }}
    </div>
    <div class="header-right">
      <HeaderCart />
    </div>
  </div>
</div>
</template>

<script>

export default {
  name: 'demo-header',
};
</script>

<style lang="postcss">
@import '../assets/css/global.css';

.header-wrap {
  background-color: $main-dark;
}
.header {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 110px;
  position: relative;
  .header-title {
    @mixin title 42px;
  }
  .header-right {
    position: absolute;
    display: flex;
    height: 100%;
    align-items: center;
    right: 40px;
  }
  @media (max-width: 568px) {
    flex-direction: column;
    height: 140px;
    &.container {
      padding: 0;
    }
    .header-right {
      position: relative;
      width: 100%;
      right: unset;
      height: auto;
      margin-top: 10px;
    }
  }
}
</style>
