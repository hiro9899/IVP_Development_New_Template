<template>
  <div class="page-style1 page-style2 light-mode default-sidebar">
    <div class="language-select">
      <vue-country-code
        @onSelect="onSelect"
        :dropdownOptions="{
          disabledDialCode: true,
        }"
        :onlyCountries="['cn', 'us']"
        :defaultCountry="getCountry"
      >
      </vue-country-code>
    </div>
    <div class="d-md-flex">
      <div class="w-40 bg-style h-100vh page-style">
        <div class="page-content">
          <div class="page-single-content">
            <div>
              <img
                src="/assets/assets/images/brand/logo.png"
                alt="img"
                class="header-brand-img mb-5"
              />
              <span class="header-brand-title">{{ $t("title") }}</span>
            </div>
            <div class="card-body text-white py-5 px-8 text-center">
              <img
                src="/assets/assets/images/png/1.png"
                alt="img"
                class="w-100 mx-auto text-center"
              />
            </div>
          </div>
        </div>
      </div>
      <router-view />
    </div>
  </div>
</template>

<script>
import Ls from "./../../services/ls";
export default {
  computed: {
    getCountry() {
      if (Ls.get("countryLang") != null) {
        return Ls.get("countryLang");
      } else {
        return "CN";
      }
    },
  },
  methods: {
    onSelect({ name, iso2, dialCode }) {
      if (iso2.toString() == "US") {
        this.$i18n.locale = "en";
        Ls.set("countryLang", iso2.toString());
      } else if (iso2.toString() == "CN") {
        this.$i18n.locale = "ch";
        Ls.set("countryLang", iso2.toString());
      }
    },
  },
};
</script>

<style scoped>
.language-select {
  position: absolute;
  top: 15px;
  right: 190px;
}
.header-brand-title {
  position: absolute;
  top: 33px;
  left: 110px;
  font-size: 20px;
  color: rgb(249 243 243);
  font-weight: 700;
}
</style>

<style>
.toast-success {
  /* background-color: #51a351; */
  background-color: #51a351 !important;
}
.toast-info {
  background-color: #2f96b4;
}
.toast-error {
  background-color: #bd362f !important;
}
.vue-country-select {
  position: relative;
  top: 12px !important;
  border: 1px !important;
  box-shadow: inset 0 1px 1px rgb(0 0 0 / 8%), 0 0 8px rgb(102 175 233 / 60%);
}
.vue-country-select .dropdown {
  -webkit-transition: 0.5s ease all;
  transition: 0.5s ease all;
}
.current .iti-flag {
  margin-right: 5px;
}
.vue-country-select:hover {
  border: 1px !important;
  border-radius: 3px;
}
.vue-country-select .dropdown:hover {
  background-color: rgb(105 154 233) !important;
  border-radius: 3px;
}
.vue-country-select .dropdown-list {
  z-index: 6 !important;
}
</style>