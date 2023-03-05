<template>
  <div v-if="!isLoading" class="flex women_page">
    <!-- Side Left -->
    <div class="product_left">
      <img class="img_product" :src="data.image" alt="" />
    </div>

    <!-- Side Right -->
    <div class="product_detail">
      <header>
        <h1 class="title product_title">{{ data.title }}</h1>
        <div class="flex product_subtitle">
          <p>{{ data.category }}</p>
          <div>
            {{ data.rating.rate }}/5
            <span
              v-for="n in Math.ceil(data.rating.rate)"
              v-bind:key="'rounded-solid' + n"
            >
              <div class="rounded-solid-rate"></div>
            </span>
            <span
              v-for="i in 5 - Math.ceil(data.rating.rate)"
              v-bind:key="'rounded' + i"
            >
              <div class="rounded-rate"></div>
            </span>
          </div>
        </div>
      </header>
      <main>
        <p>{{ data.description }}</p>
        <p class="price">${{ data.price }}</p>
        <div>
          <button class="button-buy">Buy Now</button>
          <button class="button-next-product" v-on:click="next">
            Next Product
          </button>
        </div>
      </main>
    </div>
  </div>
  <div class="root-loader" v-else>
    <div class="loader"></div>
  </div>
</template>

<script>
import "../assets/style/page.css";
export default {
  name: "WomenPage",
  props: {
    data: Object,
    nextProduct: Function,
    isLoading: Boolean,
  },
  data: function () {
    return {
      rateTopRounding: 0,
    };
  },
  methods: {
    next() {
      this.$emit("nextProduct");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.flex {
  display: flex;
  justify-content: space-between;
}
.women_page {
  padding: 32px 48px;
  margin: 0 10%;
  border-radius: 8px;
  box-shadow: rgba(14, 30, 37, 0.12) 0px 2px 4px 0px,
    rgba(14, 30, 37, 0.32) 0px 2px 16px 0px;
  background-color: var(--white);
  height: fit-content;
  color: var(--prodtittle);
  text-align: left;
}

.price {
  font-size: 20px;
  font-weight: 600;
  padding: 12px 0;
  border-top: 1px solid var(--bgun-color);
  color: var(--women-color);
}

.title {
  color: var(--women-color);
}
.button-buy {
  background-color: var(--women-color);
  color: var(--white);
  margin-right: 20px;
  border: 1px solid var(--women-color);
}
.button-next-product {
  background-color: var(--white);
  color: var(--women-color);
  margin-right: 20px;
  border: 3px solid var(--women-color);
}
.img_product {
  width: 80%;
  max-height: 100%;
}

button {
  font-size: 16px;
  font-weight: 600;
  padding: 12px 16px;
  width: 30%;
  border-radius: 4px;
  box-sizing: border-box;
  cursor: pointer;
}
.product_left {
  width: 34%;
}
.product_title {
  font-size: 28px;
  margin-bottom: 16px;
}
.product_subtitle {
  padding-bottom: 8px;
  border-bottom: 1px solid var(--bgun-color);
  margin-bottom: 24px;
}
.product_detail {
  width: 60%;
}

.rounded-solid-rate {
  display: inline-block;
  margin: 0 2px;
  width: 16px;
  height: 16px;
  border-radius: 100%;
  background-color: var(--women-color);
}
.rounded-rate {
  display: inline-block;
  margin: 0 2px;
  width: 16px;
  height: 16px;
  border: 2px solid var(--women-color);
  box-sizing: border-box;
  border-radius: 100%;
}

.loader {
  display: flex;
  border: 8px solid var(--white);
  /* Light grey */
  border-top: 8px solid var(--women-color);
  /* Blue */
  border-radius: 50%;
  width: 50px;
  height: 50px;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

.root-loader {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 100%;
}
</style>