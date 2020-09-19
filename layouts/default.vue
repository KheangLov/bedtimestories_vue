<template>
  <div>
    <b-navbar
      toggleable="lg"
      type="light"
      variant="light"
      sticky
      class="shadow-sm"
      v-bind:class="isUserScrolling ? 'top-z-index' : ''"
    >
      <b-container>
        <b-navbar-brand to="/" class="font-weight-bold">
          <b-img
            src="http://mybedtimestories.epizy.com/assets/images/icon-logo.png"
            fluid
            alt="icon-logo.png"
            class="custom-img"
          >
          </b-img>
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
    <footer class="footer">
      <b-container>
        <b-row>
          <b-col md="6">
            <b-row class="mb-3">
              <b-col sm="2" class="pr-0">
                <div class="footer-logo">
                  <b-img src="http://mybedtimestories.epizy.com/assets/images/icon-logo.png" fluid alt="icon-logo.png"></b-img>
                </div>
              </b-col>
              <b-col sm="10" class="pl-0">
                <div class="text-brand">
                  <h2 class="name"> Bedtimestories </h2>
                  <h3 class="text"> Exciting tales for young & old </h3>
                </div>
              </b-col>
            </b-row>
            <div class="text-footer mb-3">
              The storytelling app for families - read diverse <br>
              & empowering stories or tell them in your own <br>
              words.
            </div>
            <a href="#" class="cpyr-footer">
              © Little Light Studio GmbH
            </a>
          </b-col>
          <b-col cols="2">
            <h4 class="menu-title">Product</h4>
            <b-nav vertical class="nav-footer">
              <b-nav-item>Home</b-nav-item>
              <b-nav-item>Library</b-nav-item>
            </b-nav>
          </b-col>
          <b-col cols="2">
            <h4 class="menu-title">Company</h4>
            <b-nav vertical class="nav-footer">
              <b-nav-item>About Us</b-nav-item>
            </b-nav>
          </b-col>
          <b-col cols="2">
            <h4 class="menu-title">Company</h4>
            <b-nav vertical class="nav-footer">
              <b-nav-item>Facebook</b-nav-item>
              <b-nav-item>Twitter</b-nav-item>
              <b-nav-item>Instagram</b-nav-item>
            </b-nav>
          </b-col>
        </b-row>
      </b-container>
    </footer>
  </div>
</template>

<style>
.top-z-index {
  z-index: 9999 !important;
}

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
  margin-right: 5px;
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
      isUserScrolling: false,
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
  created () {
    if (process.client) {
        window.addEventListener('scroll', this.handleScroll);
    }
  },
  watch: {
    $route() {
      this.handleActive();
    }
  },
  methods: {
    handleScroll: function() {
      // Any code to be executed when the window is scrolled
      this.isUserScrolling = (window.scrollY > 0);
    },
    clearActive: function() {
      this.navItems.forEach(val => {
        val.class = 'font-weight-normal';
      });
    },
    handleActive: function() {
      const vm = this;
      this.clearActive();
      let index = _.findIndex(this.navItems, function(o) {
        return o.slug == vm.$nuxt.$route.name;
      });
      if (index < 0) index = 1;
      this.navItems[index].class += ' active';
    }
  },
  mounted() {
    this.handleActive();
  }
}
</script>
