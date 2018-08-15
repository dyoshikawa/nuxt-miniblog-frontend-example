<template>
  <section>
    <Header />
    <b-container>
      <b-card title="Welcome" class="mb-3">
        <p>This is example web application mini blog.</p>
        <router-link to="/login">
          <b-button variant="primary" class="btn-block mb-2">Login</b-button>
        </router-link>
        <router-link to="/signup">
          <b-button variant="success" class="btn-block">Signup</b-button>
        </router-link>
      </b-card>
      <div v-for="post in posts" :key="post.id">
        <b-card class="mb-2">
          <p>
            <router-link :to="`/user/${post.user_id}`">{{ post.user_name }}</router-link>
          </p>
          {{ post.content }}
        </b-card>
      </div>
    </b-container>
  </section>
</template>

<script lang="ts">
import * as axiosBase from '~/plugins/axios';
import Header from '~/components/Header.vue';
import { library } from '@fortawesome/fontawesome-svg-core';
import { faSpinner } from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';

const axios = axiosBase.getInstance();

library.add(faSpinner);

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
      isLoading: false,
      posts: []
    };
  },
  methods: {},
  async asyncData() {
    const res = await axios.get('/posts');
    return { posts: res.data.data };
  }
};
</script>