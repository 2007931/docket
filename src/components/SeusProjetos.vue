<template>
  <div class="seus-projetos">
    <span>Seus projetos:</span>
    <div class="carousel">
      <a @click="handlePrev">
        <div class="seta-prev" />
      </a>
      <div v-if="projetos.length !== 0" class="imgs-wrapper">
        <a :href="projetos[carouselIndex].url">
          <img :src="projetos[carouselIndex].download_url" />
        </a>
        <a :href="projetos[(carouselIndex + 1) % projetos.length].url">
          <img
            :src="projetos[(carouselIndex + 1) % projetos.length].download_url"
          />
        </a>
      </div>
      <a @click="handleNext">
        <div class="seta-next" />
      </a>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'SeusProjetos',
    data() {
      return {
        carouselIndex: 0,
        projetos: [],
      };
    },

    methods: {
      handleNext() {
        this.carouselIndex = (this.carouselIndex + 1) % this.projetos.length;
      },
      handlePrev() {
        this.carouselIndex === 0
          ? (this.carouselIndex = this.projetos.length - 1)
          : (this.carouselIndex -= 1);
      },
    },

    beforeMount() {
      fetch('https://picsum.photos/v2/list')
        .then((res) => res.json())
        .then((res) => (this.projetos = res));
    },
  };
</script>

<style lang="scss" scoped>
  .seus-projetos {
    span {
      text-align: left;
      font: normal normal 600 16px/24px Open Sans;
      letter-spacing: 0px;
      color: #2e2d2c;
    }
    .carousel {
      display: flex;
      gap: 20px;
      align-items: center;
      justify-content: space-between;
      a {
        cursor: pointer;
      }
      .seta-prev {
        width: 10px;
        height: 40px;
        border-right: 10px solid #c4c8cc;
        border-top: 20px solid transparent;
        border-bottom: 20px solid transparent;
        box-sizing: border-box;
      }
      .seta-next {
        width: 10px;
        height: 40px;
        border-left: 10px solid #c4c8cc;
        border-top: 20px solid transparent;
        border-bottom: 20px solid transparent;
        box-sizing: border-box;
      }
      img {
        width: 174px;
        height: 120px;
        box-shadow: 0px 3px 6px #2e2d2c66;
        border: 2px solid #ffffff;
      }
      .imgs-wrapper {
        display: grid;
        column-gap: 20px;
        grid-template-columns: repeat(auto-fit, 174px);
        grid-template-rows: 1fr 0;
        overflow: hidden;
        flex-grow: 1;
        justify-content: center;
      }
    }
  }
</style>
