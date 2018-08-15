<template>
  <section>
    <Header />
    <b-container>
      <b-card :title="user.name"
              class="mb-3"
      >
        <follow-button :is-loading="isLoadingFollow"
                       :follow="follow"
        />
        <unfollow-button :is-loading="isLoadingUnfollow"
                         :unfollow="unfollow"
        />
      </b-card>

      <div class="pagination">
        <b-pagination size="md"
                      :total-rows="meta.total"
                      v-model="currentPage"
                      :per-page="meta.per_page"
                      @change="changePosts"
        />
      </div>

      <Post v-for="post in posts"
            :post="post"
            :key="post.id"
      />
    </b-container>
  </section>
</template>

<script lang="ts">
import * as axiosBase from '~/plugins/axios';
import Header from '~/components/Header.vue';
import Post from '~/components/Post.vue';
import FollowButton from '~/components/FollowButton.vue';
import UnfollowButton from '~/components/UnfollowButton.vue';
import AllowButton from '~/components/AllowButton.vue';

const axios = axiosBase.getInstance();

export default {
  components: {
    Header,
    Post,
    FollowButton,
    UnfollowButton
  },
  data() {
    return {
      error: '',
      isLoadingFollow: false,
      isLoadingUnfollow: false,
      user: {},
      posts: [],
      meta: {},
      currentPage: 1
    };
  },
  methods: {
    async follow() {
      this.isLoadingFollow = true;
      await axios.post(`/follow/${this.user.id}`).catch(err => {
        this.error = err.response.data.error;
      });
      this.isLoadingFollow = false;
    },
    async unfollow() {
      this.isLoadingUnfollow = true;
      await axios.post(`/follow/${this.user.id}`).catch(err => {
        this.error = err.response.data.error;
      });
      this.isLoadingUnfollow = false;
    },
    async changePosts(event) {
      console.log(event);
      const res: any = await axios.get(`/posts?page=${event}`).catch(err => {
        this.error = err.response.data.message;
      });
      this.posts = res.data.data;
    }
  },
  async asyncData({ params }) {
    const userRes = await axios.get(`/users/${params.id}`);
    const postsRes = await axios.get(`/posts`);
    return {
      user: userRes.data.data,
      posts: postsRes.data.data,
      meta: postsRes.data.meta
    };
  }
};
</script>

<style scoped>
.pagination {
  display: flex;
  justify-content: center;
}
</style>
