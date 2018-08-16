<template>
  <section>
    <b-navbar toggleable="md" type="dark" variant="secondary">
      <b-container>
        <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>
        <b-navbar-brand href="/">Mini Blog</b-navbar-brand>
        <b-collapse is-nav id="nav_collapse">
          <b-navbar-nav>  
            <b-nav-item href="/timeline">
              Timeline
            </b-nav-item>
            <b-nav-item href="/following">
              Following
            </b-nav-item>
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <b-nav-item-dropdown right>
              <!-- Using button-content slot -->
              <template slot="button-content">
                <em>User</em>
              </template>
              <b-dropdown-item href="#">Mypage</b-dropdown-item>
              <b-dropdown-item href="#">Logout</b-dropdown-item>
            </b-nav-item-dropdown>
          </b-navbar-nav>

        </b-collapse>
      </b-container>
    </b-navbar>

    <b-jumbotron class="jumbotron-custom" bg-variant="info" text-variant="white">
      <b-container>
        <h1>Mini Blog</h1>
      </b-container>
    </b-jumbotron>
  </section>
</template>

<script lang="ts">
export default {};
</script>

<style scoped>
.jumbotron-custom {
  border-radius: 0;
}
</style>
