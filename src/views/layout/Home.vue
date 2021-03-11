<template>
  <div class="home">
    <left-menu />
    <div class="main-app" :class="{ 'menu-unfold': collapsed }">
      <slider-nav />
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex';
import LeftMenu from './components/Left-Menu.vue';
import SliderNav from './components/SliderNav.vue';

export default {
  data() {
    return {};
  },
  computed: {
    ...mapState(['collapsed']),
  },
  methods: {},

  components: {
    LeftMenu,
    SliderNav,
  },
};
</script>

<style  lang="less">
@import url("~@/assets/css/home.less");
</style>
