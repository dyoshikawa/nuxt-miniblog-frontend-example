<template>
  <b-card class="mb-2">
    <p>
      <router-link :to="`/users/${post.user_id}`">{{ post.user_name }}</router-link>
    </p>
    {{ post.content }}
  </b-card>
</template> 

<script>
export default {
  props: ['post']
};
</script>
