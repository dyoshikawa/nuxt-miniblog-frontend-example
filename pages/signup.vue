<template>
  <section>
    <Header />
    <b-container>
      <b-card title="Signup">
        <b-alert v-if="errors.length !== 0"
                 variant="danger"
                 show
        >
          <ul>
            <li v-for="error in errors" :key="error">{{ error[0] }}</li>
          </ul>
        </b-alert>
        <b-form-group>
          <label>Name</label>
          <b-input v-model="name" />
        </b-form-group>
        <b-form-group>
          <label>Email</label>
          <b-input v-model="email" />
        </b-form-group>
        <b-form-group>
          <label>Password</label>
          <b-input v-model="password" type="password" />
        </b-form-group>
        <b-form-group>
          <label>Password Confirmation</label>
          <b-input v-model="passwordConfirmation" type="password" />
        </b-form-group>
        <b-button variant="success"
                  @click="signup"
                  class="mr-2"
        >
          Signup
        </b-button>
        <router-link to="/login">Login?</router-link>
      </b-card>
    </b-container>
  </section>
</template>

<script lang="ts">
import * as axiosBase from '~/plugins/axios';
import Header from '~/components/Header.vue';

const axios = axiosBase.getInstance();

export default {
  components: {
    Header
  },
  data() {
    return {
      name: '',
      email: '',
      password: '',
      passwordConfirmation: '',
      errors: []
    };
  },
  methods: {
    signup: async function() {
      const res: any = await axios
        .post('/auth/signup', {
          name: this.name,
          email: this.email,
          password: this.password,
          password_confirmation: this.passwordConfirmation
        })
        .catch(error => {
          this.errors = error.response.data.errors;
          console.log(this.errors);
        });
      localStorage.setItem('jwt', res.data.access_token);
      this.$router.push('/timeline');
    }
  }
};
</script>

<style scoped>
ul {
  margin: 0;
}
</style>
