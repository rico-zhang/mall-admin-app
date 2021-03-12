<template>
  <div class="menu-list">
    <a-menu
      :default-selected-keys="['1']"
      :default-open-keys="['sub1']"
      mode="inline"
      theme="dark"
      :inline-collapsed="collapsed"
    >
      <a-sub-menu v-for="route of $store.state.menuRoutes" :key="route.name">
        <span slot="title"
          ><a-icon type="mail" /><span>{{ route.meta.title }}</span></span
        >
        <a-menu-item v-for="child of route.children" :key="child.name">{{
          child.meta.title
        }}</a-menu-item>
      </a-sub-menu>
    </a-menu>
  </div>
</template>

<script>
import { mapState } from 'vuex';

export default {
  computed: {
    ...mapState(['collapsed']),
  },
  created() {
    console.log(this.$store.state.menuRoutes);
  },
};
</script>
