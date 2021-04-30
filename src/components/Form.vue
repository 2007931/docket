<template>
  <form novalidate @submit.prevent="submitForm">
    <h2>Venha trabalhar na Docket</h2>
    <span class="action-text"
      >Preencha o formulário abaixo e venha trabalhar em uma das startups mais
      desejadas do Brasil!</span
    >
    <span class="form-title">Dados pessoais</span>
    <div class="form-input">
      <label for="name-input" class="required">Nome completo</label>
      <input
        id="name-input"
        v-model="$v.formData.nome.$model"
        type="text"
        placeholder="Seu Nome Completo"
        :class="{
          'error-input': $v.formData.nome.$error && submitStatus == 'ERROR',
        }"
      />
      <div
        v-if="submitStatus == 'ERROR' && !$v.formData.nome.required"
        class="error"
      >
        Preencha o campo acima
      </div>
    </div>

    <div class="form-input">
      <label for="email-input" class="required">E-mail</label>
      <input
        id="email-input"
        v-model="$v.formData.email.$model"
        type="email"
        placeholder="seunome@sobrenome.com.br"
        :class="{
          'error-input': $v.formData.email.$error && submitStatus == 'ERROR',
        }"
      />
      <div
        v-if="submitStatus == 'ERROR' && !$v.formData.email.required"
        class="error"
      >
        Preencha o campo acima
      </div>
      <div
        v-if="submitStatus == 'ERROR' && !$v.formData.email.email"
        class="error"
      >
        Insira um e-mail válido
      </div>
    </div>

    <div class="form-input">
      <label for="phone-input" class="required">Telefone 1</label>
      <the-mask
        id="phone-input"
        v-model="$v.formData.telefone1.$model"
        :mask="['(##) ####-####', '(##) #####-####']"
        type="tel"
        placeholder="(99) 99999-9999"
        pattern="\([0-9]{2}\) [0-9]{5}-[0-9]{4}"
        :class="{
          'error-input':
            $v.formData.telefone1.$error && submitStatus == 'ERROR',
        }"
      />
      <div
        v-if="submitStatus == 'ERROR' && !$v.formData.telefone1.required"
        class="error"
      >
        Preencha o campo acima
      </div>
      <div
        v-if="submitStatus == 'ERROR' && !$v.formData.telefone1.phone"
        class="error"
      >
        Insira um telefone válido
      </div>
    </div>

    <div class="form-input">
      <label for="phone-input">Telefone 2</label>
      <the-mask
        id="phone-input"
        v-model="$v.formData.telefone2.$model"
        :mask="['(##) ####-####', '(##) #####-####']"
        type="tel"
        placeholder="(99) 99999-9999"
        pattern="\([0-9]{2}\) [0-9]{5}-[0-9]{4}"
        :class="{
          'error-input':
            $v.formData.telefone2.$error && submitStatus == 'ERROR',
        }"
      />
    </div>

    <button><span>Enviar</span></button>
  </form>
</template>

<script>
  import { required, email } from 'vuelidate/lib/validators';
  import { validationMixin } from 'vuelidate';
  import { TheMask } from 'vue-the-mask';

  // Vuelidate não tem validation de telefone, então vamos fazer uma
  const phone = (value) => /[0-9]{10,11}$/.test(value);

  export default {
    name: 'Form',

    components: {
      TheMask,
    },

    validations: {
      formData: {
        nome: {
          required,
        },
        email: {
          required,
          email,
        },
        telefone1: {
          required,
          phone,
        },
        telefone2: {
          phone,
        },
      },
    },

    mixins: [validationMixin],

    data() {
      return {
        formSend: false,
        formData: {
          nome: null,
          email: null,
          telefone1: null,
          telefone2: null,
        },
        submitStatus: null,
      };
    },

    props: { getData: Function },

    methods: {
      async submitForm() {
        if (await this.validateForm()) {
          this.getData({ ...this.formData });
        }
      },

      validateForm() {
        this.$v.$touch();
        if (this.$v.$invalid) {
          this.submitStatus = 'ERROR';
          return false;
        } else {
          this.submitStatus = 'OK';
          return true;
        }
      },
    },
  };
</script>

<style lang="scss" scoped>
  form {
    display: flex;
    flex-direction: column;
    gap: 20px;

    h2 {
      text-align: left;
      font: normal normal bold 24px/36px Open Sans;
      letter-spacing: 0px;
      color: #2e2d2c;
      margin: 0;
    }

    .action-text {
      text-align: left;
      font: normal normal normal 14px/20px Open Sans;
      letter-spacing: 0px;
      color: #2e2d2c;
    }

    .form-title {
      text-align: left;
      font: normal normal 600 16px/24px Open Sans;
      letter-spacing: 0px;
      color: #2e2d2c;
    }

    .form-input {
      display: flex;
      flex-direction: column;
      label {
        text-align: left;
        font: normal normal normal 14px/20px Open Sans;
        letter-spacing: 0px;
        color: #2e2d2c;
      }
    }
    button {
      background: #3570b2 0% 0% no-repeat padding-box;
      box-shadow: 0px 3px 6px #2e2d2c66;
      border-radius: 20px;
      border: none;
      text-align: center;
      font: normal normal 600 16px/24px Open Sans;
      letter-spacing: 0px;
      color: #ffffff;
      padding: 9px 20px;
      width: fit-content;
      display: grid;
      place-items: center;
    }

    input {
      height: 40px;
      padding: 0 10px;
    }
  }
</style>
