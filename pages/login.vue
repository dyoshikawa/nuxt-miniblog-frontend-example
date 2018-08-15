<template>
  <section>
    <Header />
    <b-container>
      <b-card title="Login">
        <b-alert v-if="error"
                 variant="danger"
                 show
        >
          {{ error }}
        </b-alert>
        <b-form-group>
          <label>Email</label>
          <b-input v-model="email" />
        </b-form-group>
        <b-form-group>
          <label>Password</label>
          <b-input v-model="password"
                   type="password"
          />
        </b-form-group>
        <b-button variant="primary"
                  class="mr-2"
                  @click="login"
        >
          <font-awesome-icon v-if="isLoading"
                             icon="spinner"
                             spin
          />
          <span v-else>Login</span>
        </b-button>
        <router-link to="/signup">Signup?</router-link>
      </b-card>
    </b-container>
  </section>
</template>

<script lang="ts">
import * as axiosBase from '~/plugins/axios';
import Header from '~/components/Header.vue';
import { library } from '@fortawesome/fontawesome-svg-core';
import { faSpinner, faCircleNotch } from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';

const axios = axiosBase.getInstance();

library.add(faSpinner);
library.add(faCircleNotch);

export default {
  components: {
    Header,
    FontAwesomeIcon
  },
  data() {
    return {
      email: '',
      password: '',
      error: '',
      isLoading: false
    };
  },
  methods: {
    login: async function() {
      this.isLoading = true;
      const res: any = await axios
        .post('/auth/login', {
          email: this.email,
          password: this.password
        })
        .catch(error => {
          this.error = error.response.data.error;
          console.log(this.error);
        });
      this.isLoading = false;
      localStorage.setItem('jwt', res.data.access_token);
      this.$router.push('/tasks');
    }
  },
  async asyncData() {}
};
</script>