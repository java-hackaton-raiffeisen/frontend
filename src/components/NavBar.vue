<template>
  <nav v-show="isNavBarVisible" id="navbar-main is-spaced" class="navbar">
    <div class="container">
      <div class="navbar-brand">
        <a class="navbar-item" href="/">
          <img src="../assets/logo.png" width="170" height="40" />
        </a>
        <div
          class="navbar-item navbar-item-menu-toggle is-hidden-desktop burger-right"
        >
          <a @click.prevent="menuNavBarToggle">
            <b-icon :icon="menuNavBarToggleIcon" custom-size="mdi-36px" />
          </a>
        </div>
      </div>

      <div
        class="navbar-menu fadeIn animated faster"
        :class="{ 'is-active': isMenuNavBarActive }"
      >
        <div class="navbar-end">
          <div class="navbar-item">
            <div class="image image-inline is-60x60">
              <img src="../assets/person1.png" class="is-rounded" />
            </div>
            <div style="padding-left: 30px; line-height: 15px">
              <div class="has-text-left"><b>Иванов</b></div>
              <small>Иван Иванович</small>
            </div>
          </div>
          <div class="navbar-item" title="Log out" @click="logout">
            <b-button type="is-rounded">Выйти из системы</b-button>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import NavBarMenu from "@/components/NavBarMenu";
import { mapState } from "vuex";

export default {
  name: "NavBar",
  components: {
    NavBarMenu
  },
  data() {
    return {
      isMenuNavBarActive: false
    };
  },
  computed: {
    menuNavBarToggleIcon() {
      return this.isMenuNavBarActive ? "close" : "menu";
    },
    menuToggleMobileIcon() {
      return this.isAsideMobileExpanded ? "backburger" : "forwardburger";
    },
    ...mapState(["isNavBarVisible", "isAsideMobileExpanded"])
  },
  methods: {
    menuToggleMobile() {
      this.$store.commit("asideMobileStateToggle");
    },
    menuNavBarToggle() {
      this.isMenuNavBarActive = !this.isMenuNavBarActive;
    },
    logout() {
      this.$buefy.snackbar.open({
        message: "Log out clicked",
        queue: false
      });
    }
  }
};
</script>

<style>
.burger-right {
  margin-right: 0;
  margin-left: auto;
}
</style>
