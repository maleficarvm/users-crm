<template>
  <div class="wrapper">
    <header>
      <div class="navbar">
        <div class="container">
          <div class="navbar-content">
            <div class="logo">Users CRM</div>
            <ul class="navbar-list">
              <li class="navbar-item" v-for="link in links" :Key="link.title">
                <router-link
                  class="navbar-link"
                  :title="link.title"
                  :to="link.url"
                  >{{ link.title }}</router-link
                >
              </li>
            </ul>
          </div>
        </div>
      </div>
    </header>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  data() {
    return {
      links: [
        { title: "Home", url: "/" },
        { title: "Users", url: "/users" },
      ],
    };
  },
};
</script>

<style lang="scss">
.navbar-link {
  &.router-link-exact-active {
    color: rgb(66, 10, 112);
  }
}
</style>
