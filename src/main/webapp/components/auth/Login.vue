<template>
<form>
  <div class="field">
    <label class="label">Email</label>
    <div class="control">
      <input class="input" type="email" placeholder="Email" v-model="email" />
    </div>
  </div>
  <div class="field">
    <label class="label">Password</label>
    <div class="control">
      <input class="input" type="password" placeholder="Password" v-model="password" />
    </div>
  </div>
  <div class="field is-grouped">
    <div class="control">
      <input type="button" class="button is-primary" v-on:click="login" value="Login">
    </div>
    <div class="control">
      <input type="button" class="button is-text" v-on:click="cancel" value="Cancel">
    </div>
  </div>
  <error-message 
    v-if="errorMessage.length > 0" 
    header="Error Logging In" 
    v-bind:message="errorMessage" 
    v-on:close="clearError" />
</form>
</template>

<script lang="ts">
import Vue from 'vue';

import ErrorMessage from '../base/BaseErrorMessage.vue'

export default Vue.extend({
    name: 'login',
    data: function() {
        return {
            email: '',
            password: ''
        }
    },
    computed: {
      errorMessage: function() {
        return this.$store.state.errorMessage
      }
    },
    methods: {
        login: function() {
          this.$store.dispatch('user/login', { email: this.email, password: this.password })
        },
        cancel: function() {
          this.email = '';
          this.password = '';
          this.$emit('cancel')
        },
        clearError: function() {
          this.$store.dispatch('clearError')
        }
    },
    components: {
      ErrorMessage
    }
});
</script>

<style lang="scss">
@import "~bulma/sass/utilities/_all.sass";
@import "~bulma/sass/elements/button.sass";
@import "~bulma/sass/elements/form.sass";
</style>
