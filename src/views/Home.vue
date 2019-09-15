<template>
  <section class="section container">
    <modal-box
      :is-active="isModalActive"
      @cancel="modalCancel"
    />
    <title-bar>
      <span class="home-title">Клиенты</span>
      <button
        type="button"
        class="button is-rounded"
        @click.prevent="modalActivate"
      >
        Добавить клиента
      </button>
    </title-bar>

    <card-component title="Clients" class="has-table">
      <clients-table-sample dataUrl="http://127.0.0.1:8080/api/users/1/clients"/>
    </card-component>
  </section>
</template>

<script>
import Notification from "@/components/Notification";
import ClientsTableSample from "@/components/ClientsTableSample";
import CardComponent from "@/components/CardComponent";
import TitleBar from "@/components/TitleBar";
import ModalBox from "@/components/ModalBox";
export default {
  name: "clients",
  components: { TitleBar, CardComponent, ClientsTableSample, Notification, ModalBox },
  data() {
    return {
      isModalActive: false,
    };
  },

  methods: {
    modalActivate() {
      this.isModalActive = true;
      // this.$buefy.snackbar.open({
      //   message: "Confirmed",
      //   queue: false
      // });
    },
    modalCancel(){
      this.isModalActive = false;
    }
  }
};
</script>

<style lang="scss">
.home-title {
  margin-right: 20px;
}
</style>
