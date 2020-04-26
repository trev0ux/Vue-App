<style lang="sass" scoped>
  @import './login.scss';
</style>

<template>
      <f7-login-screen id="my-login-screen">
    <f7-view>
      <f7-page login-screen>
        <f7-login-screen-title>Seja bem vindo!</f7-login-screen-title>
        <f7-list form>
          <f7-list-input
            type="text"
            name="username"
            label="E-mail"
            :value="username"
            @input="username = $event.target.value"
          ></f7-list-input>
          <f7-list-input
            type="password"
            name="password"
            label="Senha"
            :value="password"
            @input="password = $event.target.value"
          ></f7-list-input>
        </f7-list>
        <f7-list class="login-button">
          <f7-button class="list-button" @click="alertLoginData"><f7-icon class="list-button__icon" f7="arrow_right"></f7-icon></f7-button>
        </f7-list>
          <f7-block-footer>
            Some text about login information.<br>Click "Sign In" to close Login Screen
          </f7-block-footer>
      </f7-page>
    </f7-view>
  </f7-login-screen>
</template>

<script>
  import { Device }  from 'framework7/framework7-lite.esm.bundle.js';

export default {
    name: 'Login',
    props: {
        msg: String,

        // Login screen data
        username: '',
        password: '',
    },                // Framework7 Parameters
        f7params: {

          data: function () {
            return {
            };
          },

          input: {
            scrollIntoViewOnFocus: Device.cordova && !Device.electron,
            scrollIntoViewCentered: Device.cordova && !Device.electron,
          },
        },

        methods: {
      alertLoginData() {
        this.$f7.dialog.alert('Username: ' + this.username + '<br>Password: ' + this.password, () => {
          this.$f7.loginScreen.close();
        });
      }
    },
        mounted() {
      this.$f7ready((f7) => {
        // Init cordova APIs (see cordova-app.js)
        if (Device.cordova) {
          cordovaApp.init(f7);
        }
        // Call F7 APIs here
      });
    }
}
</script>