<template>
  <section>
    <Header />
    <b-container>
      <b-card title="Hello, this is your page." class="mb-3">
      </b-card>

      <div class="pagination">
        <b-pagination size="md"
                      :total-rows="meta.total"
                      v-model="currentPage"
                      :per-page="meta.per_page"
                      @change="changePosts"
        />
      </div>

      <Post v-for="post in posts" :post="post"
            :key="post.id"
      />
    </b-container>
  </section>
</template>

<script lang="ts">
import * as axiosBase from '~/plugins/axios';
import Header from '~/components/Header.vue';
import Post from '~/components/Post.vue';
import { library } from '@fortawesome/fontawesome-svg-core';
import { faSpinner } from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';

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
      email: '',
      password: '',
      error: '',
      isLoading: false,
      posts: [],
      currentPage: 1,
      meta: 0
    };
  },
  methods: {
    async changePosts(event) {
      const res: any = await axios.get(`/posts?page=${event}`).catch(err => {
        this.error = err.response.data.message;
      });
      this.posts = res.data.data;
    }
  },
  async asyncData() {
    const res = await axios.get('/posts');
    return { posts: res.data.data, meta: res.data.meta };
  }
};
</script>

<style scoped>
.pagination {
  display: flex;
  justify-content: center;
}
</style>
