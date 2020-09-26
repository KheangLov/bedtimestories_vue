<template>
  <fragment>
    <h2 class="text-center font-weight-bold text-primary">Login</h2>
    <ValidationObserver ref="form">
      <b-form @submit.prevent="handleSubmit">
        <b-form-group
          id="input-group-email"
          label="Email:"
          label-for="input-email"
        >
          <ValidationProvider
            v-slot="{ errors }"
            name="email"
            type="email"
            rules="required|email"
          >
            <b-form-input
              id="input-email"
              v-model="form.email"
              type="email"
              required
              placeholder="Enter email"
              :class="errors.length ? 'border-danger' : ''"
            >
            </b-form-input>
            <span v-if="errors.length" class="text-danger">
              {{ errors[0] }}
            </span>
          </ValidationProvider>
        </b-form-group>

        <b-form-group
          id="input-group-password"
          label="Password:"
          label-for="input-password"
        >
          <ValidationProvider
            v-slot="{ errors }"
            name="password"
            type="password"
            rules="required|min:6"
          >
            <b-form-input
              id="input-password"
              v-model="form.password"
              type="password"
              required
              placeholder="Enter password"
              :class="errors.length ? 'border-danger' : ''"
            >
            </b-form-input>
            <span v-if="errors.length" class="text-danger">
              {{ errors[0] }}
            </span>
          </ValidationProvider>
        </b-form-group>
        <div class="text-center d-flex mx-auto justify-content-between">
          <b-link to="/auth/register">Register</b-link>
          <b-link to="/auth/login">Forgot password?</b-link>
        </div>
        <b-button type="submit" block variant="outline-primary mt-4">Login</b-button>
      </b-form>
    </ValidationObserver>
  </fragment>
</template>

<script>
import { Fragment } from 'vue-fragment';
import axios from 'axios';
import Noty from 'noty';
import { ValidationObserver, ValidationProvider } from "vee-validate";
export default {
  layout: 'auth',
  components: {
    Fragment,
    ValidationObserver,
    ValidationProvider
  },
  data() {
    return {
      form: {}
    };
  },
  methods: {
    handleSubmit: function() {
      this.$refs.form.validate()
        .then(success => {
          if (!success) {
            new Noty({
              text: 'Invild data!',
              type: 'error',
              timeout: 2000
            }).show();
            return false;
          }

          axios.post('http://localhost:1337/api/v1/login', this.form)
            .then(val => {
              const { data: { message, data } } = val;
              new Noty({
                text: message,
                type: data ? 'success' : 'error',
                timeout: 2000
              }).show();
            })
            .catch(err => console.log(err));

          // Wait until the models are updated in the UI
          this.$nextTick(() => {
            this.$refs.form.reset();
          });
        });
    }
  }
}
</script>
