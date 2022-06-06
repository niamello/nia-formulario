<template>
  <html>
    <body>
      <div id="app">
        <h1>{{ dados }}</h1>
        <header>
          <nav class="navigation-bar">
            <img
              class="navbar-image"
              src="../img/arrow.png"
              alt="Tecla de voltar"
            />
            <h4 class="navbar-title">Formulário</h4>
          </nav>
        </header>
        <form id="app" @submit.prevent="checkForm">
          <div class="container">
            <img :src="imageUrl" />
            <div class="container-title">
              <h1 class="title">Seja bem-vindo</h1>
              <h3 class="subtitle">Dados de contato</h3>
              <p class="text">
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Orci,
                volutpat in iaculis nec nibh sinsl tellus.
              </p>
            </div>

            <div class="name">
              <label for="name">Nome completo</label>
              <input id="name" v-model="name" type="text" name="name" />
              <p v-if="errorNameEmpty" class="textError">
                Nome não pode ser vazio
              </p>
              <p v-if="errorNameLength" class="textError">
                Nome deve ter pelo menos 5 carácteres
              </p>
            </div>

            <div class="input-group">
              <div class="input-box">
                <label for="email">Email</label>
                <input id="e-mail" v-model="email" type="email" name="email" />
                <p v-if="errorEmail" class="textError">E-mail inválido</p>
              </div>

              <div class="input-box">
                <label for="confirmeemail">Confirmar e-mail</label>
                <input id="confirmemail" v-model="confirmemail" type="email" />
                <p v-if="errorConfirmEmail" class="textError">
                  Confirmação de e-mail inválida
                </p>
              </div>
            </div>

            <div class="input-group">
              <div class="input-box">
                <label for="cpf">CPF</label>
                <input
                  v-mask="'###.###.###-##'"
                  id="cpf"
                  v-model="cpf"
                  type="text"
                  name="cpf"
                />
                <p v-if="errorCPFEmpty" class="textError">
                  CPF não pode ser vazio
                </p>
                <p v-if="errorCPFLength" class="textError">
                  CPF deve ter 11 carácteres
                </p>
              </div>

              <div class="input-box">
                <label for="cellphone">Celular</label>
                <input
                  v-mask="'+55 (##) #####-####'"
                  id="cellphone"
                  v-model="cellphone"
                  type="tel"
                  name="cellphone"
                />
                <p v-if="errorCellphoneEmpty" class="textError">
                  Celular não pode ser vazio
                </p>
                <p v-if="errorCellphoneLength" class="textError">
                  Celular deve ter 11 carácteres
                </p>
              </div>
            </div>

            <div class="input-date">
              <div class="input-box">
                <label for="date">Data de nascimento</label>
                <input
                  id="date"
                  v-model="date"
                  type="date"
                  name="date"
                  placeholder="Preencha com a sua data de nascimento"
                />
                <p v-if="errorDateLength" class="textError">
                  Data de nascimento não pode ser vazio
                </p>
              </div>
            </div>

            <p class="description-one">
              Lorem ipsum dolor sit amet, consectetur adipiscing elit.
            </p>
            <p class="description-two">
              Mattis semper odio pretium vestibulum nulla.
            </p>

            <div class="checkbox-one">
              <input type="checkbox" id="msn" value="msn" />
              <label class="social-media" for="msn">Email e MSN</label>
              <br />
            </div>

            <div class="checkbox-two">
              <input type="checkbox" id="whatsapp" value="whatsapp" />
              <label class="social-media" for="whatsapp">Whatsapp</label>
            </div>

            <p class="description-three">
              Lorem ipsum dolor sit amet, consectetur adipiscing elit. Orci,
              volutpat in iaculis nec nibh sinsl tellus. Amet tellus nunc dolor
              magna aliquet risus. Habitant neque, id risus diam.
            </p>

            <button class="form-button" click="checkForm">Continuar</button>
          </div>
        </form>

        <img class="sideimg" src="../img/felipe.jpg" alt="Imagem lateral" />
      </div>
    </body>
  </html>
</template>

<script>
import api from "../services/api";

export default {
  name: "Texts",
  props: {
    dados: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      errorNameEmpty: false,
      errorNameLength: false,
      errorEmail: false,
      errorCPFEmpty: false,
      errorCPFLength: false,
      errorCellphoneEmpty: false,
      errorCellphoneLength: false,
      errorConfirmEmail: false,
      errorDateLength: false,
      name: null,
      email: null,
      cpf: null,
      cellphone: null,
      confirmemail: null,
      date: null,
      user: {},
      imageUrl: null,
    };
  },

  methods: {
    checkName() {
      if (!this.name) {
        /*se tiver vazio*/
        this.errorNameEmpty = true;
        this.errorNameLength = false;
        return false;
      } else if (this.name.length < 3) {
        /*se não tiver o mínimo de 5 carácteres*/
        this.errorNameEmpty = false;
        this.errorNameLength = true;
        return false;
      } else {
        /*se estiver corrreto*/
        this.errorNameEmpty = false;
        this.errorNameLength = false;
        return true;
      }
    },
    checkEmail() {
      const emailRegex =
        /^[a-z0-9.]+@[a-z0-9]+\.[a-z]+(\.[a-z]+)?$/i; /*validação de e-mail - deve ter o @, algo a mais depois do @ e o ponto*/
      if (!emailRegex.test(this.email)) {
        /*se não passar no teste*/
        this.errorEmail = true;
        return false;
      } else {
        this.errorEmail = false;
        return true;
      }
    },
    checkConfirmEmail() {
      if (this.email !== this.confirmemail) {
        this.errorConfirmEmail = true;
        return false;
      } else {
        /*caso for igual*/
        this.errorConfirmEmail = false;
        return true;
      }
    },
    checkCpf() {
      if (!this.cpf) {
        /*se tiver vazio*/
        this.errorCPFLength = false;
        this.errorCPFEmpty = true;
        return false;
      } else if (this.cpf.length < 14) {
        /*se não tiver 11 carácteres*/
        this.errorCPFEmpty = false;
        this.errorCPFLength = true;
        return false;
      } else {
        /*se estiver corrreto*/
        this.errorCPFEmpty = false;
        this.errorCPFLength = false;
        return true;
      }
    },
    checkCellphone() {
      if (!this.cellphone) {
        /*se tiver vazio*/
        this.errorCellphoneLength = false;
        this.errorCellphoneEmpty = true;
        return false;
      } else if (this.cellphone.length < 14) {
        /*se não tiver 11 carácteres*/
        this.errorCellphoneEmpty = false;
        this.errorCellphoneLength = true;
        return false;
      } else {
        /*se tiver correto */
        this.errorCellphoneEmpty = false;
        this.errorCellphoneLength = false;
        return true;
      }
    },
    checkDate() {
      if (!this.date) {
        this.errorDateLength = true;
        return false;
        /*se não passar no teste*/
      } else {
        this.errorDateLength = false;
        return true;
      }
    },

    checkForm() {
      const isNameCorrect = this.checkName();
      const isEmailCorrect = this.checkEmail();
      const isConfirmEmailCorrect = this.checkConfirmEmail();
      const isCpfCorrect = this.checkCpf();
      const isCellphoneCorrect = this.checkCellphone();
      const isDateCorrect = this.checkDate();
      if (
        isNameCorrect &&
        isEmailCorrect &&
        isConfirmEmailCorrect &&
        isCpfCorrect &&
        isCellphoneCorrect &&
        isDateCorrect
      ) {
        this.sendForm();
      }
    },

    sendForm() {
      api
        .post("/customer", {
          full_name: this.name,
          email: this.email,
          email_confirmation: this.confirmemail,
          cpf: this.cpf,
          cellphone: this.cellphone,
          birthdate: this.date,
          email_sms: "test",
          whatsapp: "test2",
        })
        .then((response) => {
          console.log(response);
        })
        .catch((error) => {
          console.log("Usuário não foi cadastrado", error);
        });
    },
  },
};
</script>

<style scoped>
.navigation-bar {
  position: fixed;
  top: 0;
  background-color: rgb(224, 43, 87);
  width: 100%;
  height: 40px;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: flex;
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.212);
  color: white;
  text-transform: uppercase;
}

.container {
  width: 100%;
  display: flex;
  flex-direction: column;
  margin-top: 30px;
  color: black;
  padding: 30px 0px 30px 450px;
}

.navbar-image {
  left: 10px;
  position: fixed;
}

.container-title {
  display: flex;
  flex-direction: column;
}

.title {
  font-size: 60px;
  font-weight: 900;
}

.subtitle {
  font-size: 25px;
  margin-top: 35px;
  font-weight: 800;
}

.text {
  font-size: 15px;
  margin-top: 20px;
  font-weight: 500;
}

.name {
  margin-top: 20px;
  display: flex;
  flex-direction: column;
  max-width: 476px;
}

.input-group {
  display: flex;
  flex-direction: row;
  width: 100%;
  margin-top: 20px;
  gap: 20px;
}

.input-box {
  display: flex;
  flex-direction: column;
  max-width: 228px;
}

.input-date {
  width: 50%;
  margin-top: 20px;
}

.description-one {
  font-weight: 600;
  margin-top: 30px;
}

.description-two {
  font-weight: 600;
  margin-top: 20px;
}

.checkbox-one {
  margin-top: 30px;
}

.social-media {
  margin-left: 10px;
}

.checkbox-two {
  margin-top: 10px;
}

.description-three {
  margin-top: 30px;
  font-weight: 500;
}

.form-button {
  background-color: rgb(224, 43, 87);
  height: 40px;
  width: 120px;
  border: 0;
  border-radius: 8px;
  color: white;
  margin-top: 30px;
  font-weight: 600;
  cursor: pointer;
}

.sideimg {
  height: 700px;
  width: 400px;
  position: fixed;
  top: 0;
  left: 0;
  padding-top: 40px;
}

.sideimg div {
  padding: 8px;
  font-size: 24px;
  display: block;
}
</style>