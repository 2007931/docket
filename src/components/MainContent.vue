<template>
  <div class="main-content">
    <img src="../assets/logo.svg" />
    <div class="content-wrapper">
      <div class="form-wrapper">
        <Form :get-data="getData" />
      </div>
      <div class="results-wrapper">
        <Results :form-data="this.formData" />
      </div>
    </div>
  </div>
</template>

<script>
  import Form from './Form';
  import Results from './Results';
  export default {
    name: 'MainContent',
    components: { Form, Results },

    data() {
      return {
        formData: null,
      };
    },

    methods: {
      getData(data) {
        this.formData = data;
      },
    },
  };
</script>

<style lang="scss">
  .main-content {
    display: flex;
    gap: 30px;
    align-items: flex-start;
    flex-direction: column;
    position: relative;
    top: -200px;
    max-width: 1100px;
    margin: 10px auto;
    padding: 30px 20px;
    img {
      height: 60px;
    }

    .content-wrapper {
      display: flex;
      width: 100%;
      gap: 30px;
      flex-wrap: wrap;
      background: transparent;
      & > * {
        flex: 1;
        min-width: 250px;
        background: #ffffff 0% 0% no-repeat padding-box;
        box-shadow: 0px 1px 2px #2e2d2c66;
        border-radius: 4px;
        padding: 30px;
        &:last-child {
          background: #ebf0f5 0% 0% no-repeat padding-box;
          border: 1px solid #c4c8cc;
          border-top: 10px solid #c4c8cc;
        }
      }
    }
  }
</style>
