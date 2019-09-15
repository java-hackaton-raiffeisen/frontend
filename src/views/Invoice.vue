<template>
  <section class="section container">
    <title-bar>
      <span class="home-title">Оплата услуги</span>
    </title-bar>
    <card-component title="Clients" class="has-table">
      <div class="columns is-centered">
        <div class="column is-2" style="margin-left: 20px">
          <qr-code
            style="display: inline-block"
            text="https://e-commerce.raiffeisen.ru/vsmc3ds/pay_new/3dsproxy_init.jsp"
          ></qr-code>
        </div>
        <div class="column is-2">
          <span>
            <b> Отсканируйте QR-для оплаты услуги</b>

            <div>Клиент: Иванова Ира Владимировна</div>
            <div>Номер услуги: №101102</div>
            <div>Итоговая стоимость: 1 500 рублей</div>
            <div>Дата создания: 12.08.2019</div>
          </span>
        </div>
      </div>
    </card-component>
  </section>
</template>

<script>
import TitleBar from "@/components/TitleBar";
import CardComponent from "@/components/CardComponent";
import Vue from "vue";
import VueQRCodeComponent from "vue-qrcode-component";
Vue.component("qr-code", VueQRCodeComponent);

export default {
  components: { TitleBar, CardComponent },
  data() {}
};
</script>
