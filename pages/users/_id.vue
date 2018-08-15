<template>
  <section>
    <Header />
    <b-container>
      <b-card class="mb-3"
              :title="user.name"
      >
      </b-card>
      <Post v-for="post in posts" :post="post"
            :key="post.id"
      />
    </b-container>
  </section>
</template>

<script lang="ts">
import * as axiosBase from '~/plugins/axios';
import Header from '~/components/Header.vue';
import { library } from '@fortawesome/fontawesome-svg-core';
import { faSpinner } from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import Post from '~/components/Post.vue';

const axios = axiosBase.getInstance();

library.add(faSpinner);

export default {
  components: {
    Header,
    FontAwesomeIcon,
    Post
  },
  data() {
    return {
      error: '',
      isLoading: false,
      user: {},
      posts: []
    };
  },
  methods: {},
  async asyncData({ params }) {
    const userRes = await axios.get(`/users/${params.id}`);
    const postsRes = await axios.get(`/posts`);
    return { user: userRes.data.data, posts: postsRes.data.data };
  }
};
</script>