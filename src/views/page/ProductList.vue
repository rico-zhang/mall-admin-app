<template>
  <div class="product-list">
    <search-box @submit="submit" />
  </div>
</template>

<script>
import SearchBox from '@/components/Search.vue';

export default {
  components: {
    SearchBox,
  },
  methods: {
    submit(data) {
      console.log(data);
    },
  },
};
</script>
