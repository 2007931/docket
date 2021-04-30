<template>
  <div class="results">
    <h2>Ficha do candidato</h2>
    <div v-if="formData" class="form-mirror">
      <div class="one-area">
        <span class="label">Nome completo:</span>
        <span class="value">{{ formData.nome }}</span>
      </div>
      <div class="one-area">
        <span class="label">E-mail:</span>
        <span class="value">{{ formData.email }}</span>
      </div>
      <div class="one-area">
        <span class="label">Telefone 1:</span>
        <span class="value">{{ formData.telefone1 }}</span>
      </div>
      <div class="one-area">
        <span class="label">Telefone 2:</span>
        <span class="value">{{ formData.telefone2 }}</span>
      </div>
    </div>
    <div v-else>
      <span class="preencha"
        >Preencha o formulário e clique em "Enviar" após conferir
        atentamente.</span
      >
    </div>
    <SeusProjetos />
  </div>
</template>
<script>
  import SeusProjetos from './SeusProjetos';
  export default {
    name: 'Results',
    components: { SeusProjetos },
    props: { formData: [Object, null] },
  };
</script>
<style lang="scss" scoped>
  .results {
    display: flex;
    flex-direction: column;
    height: 100%;
    justify-content: space-between;
  }
  h2 {
    margin: 0;
    text-align: left;
    font: normal normal bold 20px/30px Open Sans;
    letter-spacing: 0px;
    color: #403d70;
    text-transform: uppercase;
    & + div {
      flex-grow: 1;
      margin-top: 20px;
    }
  }
  .preencha {
    font: italic normal normal 14px/20px Open Sans;
    letter-spacing: 0px;
    color: #ababab;
  }
  .form-mirror {
    display: flex;
    flex-direction: column;
    gap: 1em;
    .one-area {
      display: flex;
      flex-direction: column;
      .label {
        font: normal normal normal 14px/20px Open Sans;
      }
      .value {
        font: normal normal 600 14px/20px Open Sans;
      }
    }
  }
</style>
