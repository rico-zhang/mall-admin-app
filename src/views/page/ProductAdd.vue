<template>
  <div class="product-detail">
    <a-steps :current="current" class="product-step">
      <a-step v-for="item in steps" :key="item.title" :title="item.title" />
    </a-steps>
    <div class="steps-content">
      <component :is="steps[current].cmpName" @next="next" />
    </div>
  </div>
</template>

<script>
import BasicDetail from '@/components/BasicDetail.vue';
import SaleDetail from '@/components/SaleDetail.vue';

export default {
  data() {
    return {
      current: 0,
      steps: [
        {
          title: '填写基本商品信息',
          cmpName: 'BasicDetail',
        },
        {
          title: '填写商品销售信息',
          cmpName: 'SaleDetail',
        },
      ],
    };
  },
  methods: {
    next(form) {
      this.current += 1;
      console.log(form);
    },
    prev() {
      this.current -= 1;
    },
  },
  components: {
    BasicDetail,
    SaleDetail,
  },
};
</script>
<style scoped lang="less">
.product-detail {
  .product-step {
    width: 50%;
    margin: 20px auto;
  }
  .steps-content {
    margin-top: 16px;
    border: 1px dashed #e9e9e9;
    border-radius: 6px;
    background-color: #fafafa;
    min-height: 200px;
    text-align: center;
    padding-top: 80px;
  }

  .steps-action {
    margin-top: 24px;
  }
}
</style>
