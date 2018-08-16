<template>
<section>
  <b-navbar toggleable="md" type="dark" variant="secondary">
      <b-container>
        <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>
        <b-navbar-brand href="/">Dashboard</b-navbar-brand>
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
              <b-dropdown-item href="/mypage">Mypage</b-dropdown-item>
              <b-dropdown-item href="#">Logout</b-dropdown-item>
            </b-nav-item-dropdown>
          </b-navbar-nav>

        </b-collapse>
      </b-container>
    </b-navbar>
</section>
</template>

<script>
export default {};
</script>

<style>
</style>
