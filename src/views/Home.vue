<template>
  <section class="section">
    <title-bar>
      Список клиентов
    </title-bar>

    <card-component class="has-table">
      <clients-table-sample />
    </card-component>
  </section>
</template>

<script>
import Notification from "@/components/Notification";
import ClientsTableSample from "@/components/ClientsTableSample";
import CardComponent from "@/components/CardComponent";
import TitleBar from "@/components/TitleBar";
export default {
  name: "clients",
  components: { TitleBar, CardComponent, ClientsTableSample, Notification }
};
</script>
