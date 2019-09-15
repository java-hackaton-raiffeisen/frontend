<template>
  <div>
    <b-table
      :checkable="checkable"
      :loading="isLoading"
      :paginated="paginated"
      :per-page="perPage"
      default-sort="id"
      :data="services"
    >
      <template slot-scope="props">
        <b-table-column label="Номер услуги" field="id" sortable>
          №{{ props.row.id }}
        </b-table-column>
        <b-table-column label="Стоимость услуги" field="price" sortable>
          {{ props.row.price }} руб
        </b-table-column>
        <b-table-column label="Итоговая стоимость" field="fullPrice" sortable>
          {{ props.row.fullPrice }} руб
        </b-table-column>
        <b-table-column label="Услуга оплачена" field="isPayed" sortable>
          {{ props.row.isPayed ? "Да" : "Нет" }}
        </b-table-column>
        <b-table-column label="Дата создания" field="created" sortable>
          {{ props.row.created }}
        </b-table-column>
        <b-table-column label="Дата оплаты" field="payedDate" sortable>
          {{ props.row.payedDate }}
        </b-table-column>
        <b-table-column custom-key="actions" class="is-actions-cell">
          <div class="buttons space-evenly">
            <router-link
              :to="{ name: 'invoice', params: { serviceId: props.row.id } }"
              class="button is-rounded"
              type="button"
              :disabled="props.row.isPayed"
            >
              Запросить оплату
            </router-link>
            <a @click.prevent="trashModal(props.row)">
              Удалить услугу
            </a>
          </div>
        </b-table-column>
      </template>

      <section class="section" slot="empty">
        <div class="content has-text-grey has-text-centered">
          <template v-if="isLoading">
            <p>
              <b-icon icon="dots-horizontal" size="is-large" />
            </p>
            <p>Загрузка...</p>
          </template>
          <template v-else>
            <p>
              <b-icon icon="emoticon-sad" size="is-large" />
            </p>
            <p>Пока нет услуг&hellip;</p>
          </template>
        </div>
      </section>
    </b-table>
  </div>
</template>

<script>
import axios from "axios";
import ModalBox from "@/components/ModalBox";

export default {
  name: "ClientsTableSample",
  components: { ModalBox },
  props: {
    dataUrl: {
      type: String,
      default: null
    },
    checkable: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      isModalActive: false,
      trashObject: null,
      services: [
        {
          id: 101102,
          price: 1000,
          fullPrice: 1500,
          isPayed: true,
          created: "2019-07-23",
          payedDate: "2019-07-23"
        },
        {
          id: 101103,
          price: 9000,
          fullPrice: 9500,
          isPayed: false,
          created: "2019-07-23",
          payedDate: "2019-07-23"
        }
      ],
      isLoading: false,
      paginated: false,
      perPage: 10
    };
  },
  computed: {
    trashObjectName() {
      if (this.trashObject) {
        return this.trashObject.name;
      }

      return null;
    }
  },
  mounted() {
    if (this.dataUrl) {
      this.isLoading = true;
      axios
        .get(this.dataUrl)
        .then(r => {
          this.isLoading = false;
          if (r.data && r.data.data) {
            if (r.data.data.length > this.perPage) {
              this.paginated = true;
            }
            this.clients = r.data.data;
          }
        })
        .catch(e => {
          this.isLoading = false;
          this.$buefy.toast.open({
            message: `Error: ${e.message}`,
            type: "is-danger"
          });
        });
    }
  },
  methods: {
    trashModal(trashObject) {
      this.trashObject = trashObject;
      this.isModalActive = true;
    },
    trashConfirm() {
      this.isModalActive = false;
      this.$buefy.snackbar.open({
        message: "Confirmed",
        queue: false
      });
    },
    trashCancel() {
      this.isModalActive = false;
    }
  }
};
</script>
<style lang="scss">
@import "~bulma/sass/utilities/mixins.sass";

@include desktop {
  table.table {
    border-collapse: separate;
    border-spacing: 0 20px;
    background-color: #f5f5f5;
  }
  tbody > tr {
    height: 120px;
    box-shadow: 0px 2px 10px rgba(229, 229, 229, 0.5);
    border-radius: 20px;
    background-color: white;
  }
  table.table td,
  table.table th {
    justify-content: center;
    vertical-align: middle;
    text-align: center;
    border: 0;
  }
  .b-table table.table th .th-wrap {
    justify-content: center;
  }
  .buttons > button.button {
    margin-bottom: 0;
  }
  .space-evenly {
    justify-content: space-evenly;
  }
  td:first-child {
    border-left-style: solid;
    border-top-left-radius: 20px;
    border-bottom-left-radius: 20px;
  }
  td:last-child {
    border-right-style: solid;
    border-bottom-right-radius: 20px;
    border-top-right-radius: 20px;
  }
}
.image img.is-rounded {
  border-radius: 1000px;
}
.image-inline {
  display: inline-block;
}
</style>
