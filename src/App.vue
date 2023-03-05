<template>
  <div id="app" v-if="data !== null">
    <div v-if="data.category === 'men\'s clothing'" class="bgm">
      <MenPage
        :isLoading="isLoading"
        :data="data"
        @nextProduct="addPageIndex"
      />
    </div>

    <div v-if="data.category == 'women\'s clothing'" class="bgwm">
      <WomenPage
        :isLoading="isLoading"
        :data="data"
        @nextProduct="addPageIndex"
      />
    </div>

    <div
      v-if="
        data.category !== 'women\'s clothing' &&
        data.category !== 'men\'s clothing'
      "
      class="bgun"
    >
      <UnavailablePage :isLoading="isLoading" @nextProduct="addPageIndex" />
    </div>
  </div>
</template>

<script>
import MenPage from "./components/MenPage.vue";
import WomenPage from "./components/WomenPage.vue";
import UnavailablePage from "./components/UnavailablePage.vue";

export default {
  name: "App",
  data: function () {
    return {
      pageIndex: 1,
      data: null,
      isLoading: true,
    };
  },

  methods: {
    async getData(index) {
      this.isLoading = true;
      const res = await fetch(`https://fakestoreapi.com/products/${index}`);
      const finalRes = await res.json();
      this.isLoading = false;
      this.data = finalRes;
    },
    addPageIndex() {
      this.pageIndex++;
      if (this.pageIndex > 20) {
        this.pageIndex = 1;
        this.getData(this.pageIndex);
      } else {
        this.getData(this.pageIndex);
      }
    },
  },
  mounted() {
    this.getData(this.pageIndex);
  },
  components: {
    MenPage,
    WomenPage,
    UnavailablePage,
  },
};
</script>

<style></style>