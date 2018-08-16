<template>
  <section>
    <nav-bar />
    <Header />
    <b-container>
      <b-card title="Create Your Post" class="mb-3">
        <b-form-group>
          <b-textarea v-model="content" />
        </b-form-group>
        <b-button variant="primary"
                  @click="createPost"
        >
          Post
        </b-button>
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
import NavBar from '~/components/NavBar.vue';
import Header from '~/components/Header.vue';
import Post from '~/components/Post.vue';
import { library } from '@fortawesome/fontawesome-svg-core';
import { faSpinner } from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';

const axios = axiosBase.getInstance();

library.add(faSpinner);

export default {
  components: {
    NavBar,
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
      meta: {},
      content: ''
    };
  },
  methods: {
    async changePosts(event) {
      const res: any = await axios.get(`/posts?page=${event}`).catch(err => {
        this.error = err.response.data.message;
      });
      this.posts = res.data.data;
    },
    async createPost() {
      await axios
        .post(
          `/posts`,
          { content: this.content },
          {
            headers: { Authorization: `Bearer ${localStorage.getItem('jwt')}` }
          }
        )
        .catch(error => {
          console.log(error);
        });
      this.content = '';
      const res = await axios.get('/following/posts', {
        headers: {
          Authorization: `Bearer ${localStorage.getItem('jwt')}`
        }
      });
      this.currentPage = 1;
      this.posts = res.data.data;
    }
  },
  async created() {
    await axios
      .post('/auth/me', null, {
        headers: { Authorization: `Bearer ${localStorage.getItem('jwt')}` }
      })
      .catch(error => {
        this.$router.push('/');
      });

    const res = await axios.get('/following/posts', {
      headers: {
        Authorization: `Bearer ${localStorage.getItem('jwt')}`
      }
    });
    this.posts = res.data.data;
    this.meta = res.data.meta;
  }
};
</script>

<style scoped>
.pagination {
  display: flex;
  justify-content: center;
}
</style>
