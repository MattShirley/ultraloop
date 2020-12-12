<template>
  <div id="app">
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/watch">Watch</router-link>
    </div> -->
      <b-button class="nav-base" v-b-toggle.sidebar-right><b-icon-arrow-down-left-square-fill></b-icon-arrow-down-left-square-fill></b-button>
      <b-sidebar id="sidebar-right" title="Sidebar" right shadow>
        <b-nav vertical>
          <b-nav-item to="/">Watch</b-nav-item>
          <b-nav-item to="/schedule">Schedule</b-nav-item>
          <b-nav-item to="/about">About</b-nav-item>
        </b-nav>
      </b-sidebar>
    <router-view/>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        items: [
          {
            text: 'Admin',
            href: '#'
          },
          {
            text: 'Manage',
            href: '#'
          },
          {
            text: 'Library',
            active: true
          }
        ]
      }
    }
  }
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

  #nav {
    padding: 30px;

    a {
      font-weight: bold;
      color: #2c3e50;

      &.router-link-exact-active {
        color: #42b983;
      }
    }
  }

  .nav-base {
    position: absolute;
    top: 0px;
    right: 0px;
    z-index: 1000;
  }
</style>
