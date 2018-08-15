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

      <Post v-for="post in posts"
            :post="post"
            :key="post.id"
      />

      <div class="allows">
        <allow-button direction="left" />
        <allow-button direction="right" />
      </div>
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
    UnfollowButton,
    AllowButton
  },
  data() {
    return {
      error: '',
      isLoadingFollow: false,
      isLoadingUnfollow: false,
      user: {},
      posts: []
    };
  },
  methods: {
    follow: async function() {
      this.isLoadingFollow = true;
      await axios.post(`/follow/${this.user.id}`).catch(err => {
        this.error = err.response.data.error;
      });
      this.isLoadingFollow = false;
    },
    unfollow: async function() {
      this.isLoadingUnfollow = true;
      await axios.post(`/follow/${this.user.id}`).catch(err => {
        this.error = err.response.data.error;
      });
      this.isLoadingUnfollow = false;
    }
  },
  async asyncData({ params }) {
    const userRes = await axios.get(`/users/${params.id}`);
    const postsRes = await axios.get(`/posts`);
    return { user: userRes.data.data, posts: postsRes.data.data };
  }
};
</script>

<style scoped>
.allows {
  display: flex;
  justify-content: space-between;
}
</style>
