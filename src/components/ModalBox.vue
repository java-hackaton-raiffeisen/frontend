<template>
  <b-modal :active.sync="isModalActive" :width="640">
    <div class="card">
      <div class="card-content">
        <div class="container">
          <div class="columns">
            <div class="column">
              <span class="is-size-4">Добавление клиента</span>
            </div>
          </div>
          <div class="columns">
            <div class="column">
              <form>
                <div class="field">
                  <label for="" class="label"
                    >Фамилия <span class="has-text-primary">*</span></label
                  >
                  <div class="control">
                    <input
                      type="text"
                      placeholder=""
                      class="input"
                      required
                    />
                  </div>
                </div>
                <div class="field">
                  <label for="" class="label"
                    >Имя<span class="has-text-primary">*</span></label
                  >
                  <div class="control">
                    <input
                      type="text"
                      placeholder=""
                      class="input"
                      required
                    />
                  </div>
                </div>
                <div class="field">
                  <label for="" class="label">Отчество</label>
                  <div class="control">
                    <input
                      type="text"
                      placeholder=""
                      class="input"
                    />
                  </div>
                </div>
                <div class="field">
                  <label for="" class="label"
                    >Телефон<span class="has-text-primary">*</span></label
                  >
                  <div class="control">
                    <input
                      type="text"
                      placeholder=""
                      class="input"
                      required
                    />
                  </div>
                </div>
                <div class="field">
                  <label for="" class="label">Email</label>
                  <div class="control">
                    <input
                      type="email"
                      placeholder=""
                      class="input"
                    />
                  </div>
                </div>
                <div class="field">
                  <div class="buttons is-centered">
                    <button class="button">
                      Добавить клиента
                    </button>
                    <button class="button is-white">Отмена</button>
                  </div>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </b-modal>
</template>

<script>
export default {
  name: "ModalBox",
  props: {
    isActive: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      isModalActive: false
    };
  },
  methods: {
    cancel() {
      this.$emit("cancel");
    },
    confirm() {
      this.$emit("confirm");
    }
  },
  watch: {
    isActive(newValue) {
      this.isModalActive = newValue;
    },
    isModalActive(newValue) {
      if (!newValue) {
        this.cancel();
      }
    }
  }
};
</script>
