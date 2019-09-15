<template>
  <section class="section container">
    <service-modal-box
            :is-active="isModalActive"
            @cancel="modalCancel"
    />
    <title-bar>
      <span class="home-title">Список услуг </span>
      <button
              type="button"
              class="button is-rounded"
              @click.prevent="modalActivate"
      >
        Добавить услугу
      </button>
    </title-bar>

    <card-component title="services" class="has-table">
      <services-table dataUrl="http://127.0.0.1:8080/api/users/1/clients"/>
    </card-component>
  </section>
</template>
<script>
  import Notification from "@/components/Notification";
  import ServicesTable from "@/components/ServicesTable";
  import CardComponent from "@/components/CardComponent";
  import TitleBar from "@/components/TitleBar";
  import ServiceModalBox from "@/components/ServiceModalBox";
  export default {
    components: { TitleBar, CardComponent, ServicesTable, Notification, ServiceModalBox },
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

