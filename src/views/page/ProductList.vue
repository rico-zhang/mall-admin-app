<template>
  <div class="product-list">
    <search-box :categoryList="categoryList" @submit="submit" />
    <product-table :data="tableData" :page="page" @changePage="changePage" />
  </div>
</template>

<script>
import SearchBox from '@/components/Search.vue';
import ProductTable from '@/components/ProductTable.vue';

import productApi from '@/api/product';
import categoryApi from '@/api/category';

export default {
  data() {
    return {
      searchForm: {},
      tableData: [],
      defaultPage: {
        current: 1,
        pageSize: 5,
        showSizeChanger: true,
        total: 1,
        pageSizeOptions: ['5', '10', '20', '30', '40'],
      },
      page: {},
      categoryList: [],
      categoryMap: new Map(),
    };
  },
  components: {
    SearchBox,
    ProductTable,
  },
  methods: {
    submit(form) {
      this.searchForm = form;
      this.page = this.defaultPage;
      this.getTableData();
    },
    getTableData() {
      return productApi
        .list({
          page: this.page.current,
          size: this.page.pageSize,
          ...this.searchForm,
        })
        .then((res) => {
          this.page.total = res.total;
          this.tableData = res.data.map((item) => Object.assign(item, {
            categoryName: this.categoryMap.get(item.category),
          }));
        });
    },
    changePage(page) {
      this.page = page;
      this.getTableData();
    },
    getCategoryList() {
      return categoryApi.list().then((res) => {
        this.categoryList = res.data;
        const map = this.categoryList.map((item) => [item.id, item.name]);
        this.categoryMap = new Map(map);
      });
    },
  },
  async created() {
    this.page = this.defaultPage;
    await this.getCategoryList();
    this.getTableData();
  },
};
</script>
