<template>
  <div>
    <b-navbar toggleable="lg" type="light" variant="light">
      <b-container>
        <b-navbar-brand to="/" class="font-weight-bold">
          <img src="http://mybedtimestories.epizy.com/assets/images/icon-logo.png" alt="icon-logo.png" class="custom-img">
          Bedtimestories
        </b-navbar-brand>
        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav class="ml-auto">
            <b-nav-item
              v-for="(item, index) in navItems"
              @click="handleActive"
              :to="item.link"
              :class="item.class"
              :key="index"
              no-prefetch
              exact
            >
              {{ item.text }}
            </b-nav-item>
          </b-navbar-nav>
        </b-collapse>
      </b-container>
    </b-navbar>
    <Nuxt />
  </div>
</template>

<style>
.font-weight-normal {
  font-weight: 600 !important;
}

.navbar-brand {
  font-size: 1.75rem;
  color: #777 !important;
}

.custom-img {
  height: 32px;
}

.navbar-light .navbar-nav .nav-link {
  padding: 0;
  font-size: 18px;
  color: #777 !important;
}

.navbar-light .navbar-nav .nav-item {
  border-radius: 4px;
  padding: 15px 25px;
  margin: 0;
  border: 2px solid transparent;
}

.navbar-light .navbar-nav .nav-item.active,
.navbar-light .navbar-nav .nav-item:hover,
.navbar-light .navbar-nav .nav-item:focus {
  background-color: #eaeaea;
  border: 2px solid transparent;
}
</style>

<script>
import _ from 'lodash';
export default {
  data() {
    return {
      navItems: [
        {
          link: '/',
          class: 'font-weight-normal',
          text: 'Home',
          slug: 'index'
        },
        {
          link: '/library',
          class: 'font-weight-normal',
          text: 'Library',
          slug: 'library'
        },
        {
          link: '/about',
          class: 'font-weight-normal',
          text: 'About Us',
          slug: 'about'
        },
      ]
    };
  },
  watch: {
    $route() {
      this.handleActive();
    }
  },
  methods: {
    clearActive: function() {
      this.navItems.forEach(val => {
        val.class = 'font-weight-normal';
      });
    },
    handleActive: function() {
      const vm = this;
      this.clearActive();
      const index = _.findIndex(this.navItems, function(o) {
        return o.slug == vm.$nuxt.$route.name;
      });
      this.navItems[index].class += ' active';
    }
  },
  mounted() {
    this.handleActive();
  }
}
</script>
