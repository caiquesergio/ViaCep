<template>
  <div>
    <div class="header">
      <div class="adress">
        <img src="../assets/image-default.png" alt="" class="image-default" />
        <p class="text-header">Surreal São Paulo</p>
        <p class="text-header-vtex">VTEX</p>
      </div>
      <div class="header-user">
        <img src="../assets/bell.png" alt="" class="bell" />
        <div class="partition"></div>
        <img src="../assets/user.png" alt="" class="user" />
        <p class="user-text">Olá Joaquim</p>
      </div>
    </div>
    <div class="body-page">
      <img src="../assets/search.png" alt="" class="icon-search" />
      <img src="../assets/paste.png" alt="" class="icon-paste" />
      <div class="config">
        <img src="../assets/config.png" alt="" class="icon-config" />
      </div>
    </div>
    <div>
      <input
        type="text"
        placeholder="Insira o CEP"
        class="input-cep"
        id="cep"
        name="cep"
        v-model="cep"
        maxlength="8"
      />
      <ButtonCep :textButton="'Adicionar Endereço'" @click="addCep()" />

      <div class="ceps-listeds">
        <div :key="index" v-for="(item, index) in ceps">
          <p class="cep-add" v-if="item.cep">
            <img src="../assets/pin.png" alt="" class="icon-pin" /> CEP:
            <span class="cep-add-number">{{ item.cep }}</span>
          </p>
        </div>
      </div>
    </div>

    <div>
      <!-- <input type="text" v-model="cep" @keyup="getCep()" placeholder="digite o cep aqui"> -->
      <ButtonCep
        :textButton="'Gerar Endereços'"
        class="button-generate"
        @click="getCep()"
      />

      <div class="cards-generate">
        <div class="card-cep" :key="index" v-for="(item, index) in data">
          <div style="display: flex">
            <img src="../assets/pin.png" alt="" class="pin-card" />
            <p class="logradouro">{{ item.logradouro }}</p>
            <p class="locale-uf">{{ item.localidade }} - {{ item.uf }}</p>
            <p class="cep">{{ item.cep }}</p>
          </div>
          <div class="divisor-card"></div>
          <img
            @click="deleteCep(index)"
            src="../assets/trash.png"
            alt=""
            class="icon-trash"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ButtonCep from "./ButtonCep.vue";
import axios from "axios";
export default {
  data() {
    return {
      ceps: [{ cep: "" }],
      cep: "",
      data: [],
    };
  },
  components: {
    ButtonCep,
  },
  methods: {
    addCep() {
      var input = document.getElementById("cep");

      if (input.value !== "") {
        this.ceps.push({
          cep: input.value,
        });
        console.log(this.ceps);
      }
      input.value = "";
    },
    getCep() {
      if (this.cep.length == 8) {
        this.ceps.forEach((item) => {
          axios
            .get(`https://viacep.com.br/ws/${item.cep}/json/`)
            .then((response) => this.data.push(response.data))
            .catch((error) => console.log(error));
        });
      }
      //console.log(JSON.stringify(this.data));
    },
    deleteCep(index) {
      this.data.splice(index, 1);
    },
  },
};
</script>

<style scoped>
.header {
  position: absolute;
  width: 1920px;
  height: 80px;
  left: 0px;
  top: 0px;
  background: #9206e9;
}
.adress {
  box-sizing: border-box;
  position: absolute;
  width: 287px;
  height: 58px;
  left: 98px;
  top: 11px;
  border: 2px solid #ffffff;
  border-radius: 10px;
}
.text-header {
  padding-top: 7px;
  padding-left: 10px;
  margin: 0;
  width: 140px;
  height: 22px;
  left: 114px;
  top: 21px;
  font-family: "Open Sans";
  font-style: normal;
  font-weight: 700;
  font-size: 16px;
  line-height: 22px;
  display: flex;
  align-items: center;
  color: #ffffff;
}
.text-header-vtex {
  padding-left: 10px;
  margin: 0;
  width: 29px;
  height: 16px;
  left: 114px;
  top: 43px;
  font-family: "Open Sans";
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  line-height: 16px;
  display: flex;
  align-items: center;
  letter-spacing: 0.02em;
  color: #ffffff;
}
.user {
  position: absolute;
  width: 54px;
  height: 54px;
  left: 1810px;
  top: 13px;
  opacity: 10.4;
}
.user-text {
  position: absolute;
  width: 103px;
  height: 22px;
  left: 1703px;
  top: 15px;
  font-family: "Open Sans";
  font-style: normal;
  font-weight: 700;
  font-size: 16px;
  line-height: 22px;
  display: flex;
  align-items: center;
  color: #ffffff;
}
.partition {
  position: absolute;
  width: 0px;
  height: 80px;
  left: 1660px;
  top: 0px;
  opacity: 0.2;
  border: 2px solid #ffffff;
}
.bell {
  position: absolute;
  left: 82.67%;
  right: 16.67%;
  top: 33.5%;
  bottom: 12.5%;
}
.body-page {
  position: absolute;
  left: 0%;
  right: 95%;
  top: 9.18%;
  bottom: 0%;
  background: #f7f7f7;
}
.icon-search {
  padding-left: 24px;
  display: block;
  padding-top: 40px;
  padding-bottom: 50px;
}
.image-default {
  position: absolute;
  width: 54px;
  height: 54px;
  left: -80px;
  top: 0px;
  opacity: 10.4;
}
.input-cep {
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  padding: 16px;
  gap: 10px;
  position: absolute;
  width: 293px;
  height: 52px;
  left: 143px;
  top: 121px;
  border: 2px solid #bbc4ce;
  border-radius: 10px;
}
.button-generate {
  margin: 0;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  padding: 16px 211px;
  gap: 10px;
  position: absolute;
  width: 0px;
  height: 20px;
  left: 460px;
  top: 358px;
  background: #b600ee;
  border-radius: 8px;
  padding-left: 140px;
  padding-right: 140px;
}
.cep-add {
  width: 140px;
  left: 11.36%;
  right: 82.34%;
  top: 22.74%;
  bottom: 76.84%;
  font-family: "Open Sans";
  font-style: normal;
  font-weight: 700;
  font-size: 20px;
  line-height: 27px;
  display: flex;
  align-items: center;
  color: #20272c;
}
.cep-add-number {
  color: #75818c;
  margin-left: 5px;
}
.icon-pin {
  margin-right: 15px;
}
.card-cep {
  display: flex;
  margin-top: 40px;
  width: 609px;
  height: 120px;
  left: 143px;
  top: 512px;
  background: #ffffff;
  box-shadow: 0px 4px 20px rgb(32 39 44 / 10%);
  border-radius: 8px;
}
.logradouro {
  width: 410px;
  margin-top: 40px;
  font-family: "Open Sans";
  font-style: normal;
  font-weight: 700;
  font-size: 20px;
  line-height: 27px;
  color: #424e59;
  margin-left: 20px;
  text-align: start;
}
.pin-card {
  margin-top: 40px;
  height: 30px;
  width: 20px;
  margin-left: 30px;
}
.locale-uf {
  width: 200px;
  margin-top: 70px;
  margin-left: -413px;
  font-family: "Open Sans";
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 22px;
  letter-spacing: 0.01em;
  color: #20272c;
  text-align: start;
}
.cep {
  margin-top: 50px;
  margin-left: 170px;
  font-family: "Open Sans";
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 22px;
  letter-spacing: 0.01em;
  color: #b600ee;
}
.divisor-card {
  margin-left: 20px;
  width: 0px;
  height: 96px;
  left: 688px;
  top: 660px;
  border: 2px solid #e0e6ea;
  margin-top: 10px;
}
.icon-trash {
  margin-top: 46px;
  width: 22px;
  cursor: pointer;
  height: 24px;
  margin-left: 20px;
}
.ceps-listeds {
  margin-left: 140px;
  margin-top: 190px;
}
.config {
  width: 67px;
  height: 70px;
  left: 15px;
  top: 1018px;
  background: #20272c;
  border-radius: 10px;
  margin-left: 10px;
  margin-top: 510px;
}
.icon-config {
  margin-top: 15px;
  margin-left: 15px;
}
.icon-paste {
  margin-left: 24px;
}
.cards-generate {
  margin-left: 140px;
  margin-top: 250px;
}
.header-user {
  display: flex;
}
</style>
