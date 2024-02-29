<template>

  <header
    id="header"
    ref="header"
  >

    <b-navbar
      toggleable="lg"
      fixed="top"
      :style="[
        {padding: `${scrollPosition > 80 ? '0' : '5px'} 0`}
      ]"
    >
      <b-container fluid="xl" class="justify-content-between">
        <NuxtLink to="/" class="navbar-brand">
          <app-logo :height="scrollPosition > 80 ? 44 : 50" />
        </NuxtLink>

        <b-navbar-toggle target="nav-collapse">
          <template #default="{ expanded }">
            <div id="hamburger-9" class="hamburger" :class="{'is-active': expanded}">
              <span class="line"></span>
              <span class="line"></span>
              <span class="line"></span>
            </div>
<!--            <b-icon v-if="expanded" icon="chevron-bar-up"></b-icon>-->
<!--            <b-icon v-else icon="chevron-bar-down"></b-icon>-->
          </template>
        </b-navbar-toggle>

        <b-collapse
          id="nav-collapse"
          class="justify-content-end"
          is-nav
        >
          <b-navbar-nav class="ml-auto">
            <b-nav-text class="nav-link"><NuxtLink to="/about">About</NuxtLink></b-nav-text>
            <b-nav-text class="nav-link"><NuxtLink to="/blog">Blog</NuxtLink></b-nav-text>
            <b-nav-text class="nav-link"><NuxtLink to="/reviews">Reviews</NuxtLink></b-nav-text>


<!--            <b-nav-item class="nav-link scrollto active" href="#hero">Home</b-nav-item>-->
<!--            <b-nav-item class="nav-link scrollto" href="#about">About</b-nav-item>-->


          </b-navbar-nav>

          <!--        <b-navbar-nav class="ml-auto">-->


          <!--          <b-nav-item-dropdown text="Lang" right>-->
          <!--            <b-dropdown-item href="#">EN</b-dropdown-item>-->
          <!--            <b-dropdown-item href="#">ES</b-dropdown-item>-->
          <!--            <b-dropdown-item href="#">RU</b-dropdown-item>-->
          <!--            <b-dropdown-item href="#">FA</b-dropdown-item>-->
          <!--          </b-nav-item-dropdown>-->

          <!--          <b-nav-item-dropdown right>-->
          <!--            &lt;!&ndash; Using 'button-global' slot &ndash;&gt;-->
          <!--            <template #button-global>-->
          <!--              <em>User</em>-->
          <!--            </template>-->
          <!--            <b-dropdown-item href="#">Profile</b-dropdown-item>-->
          <!--            <b-dropdown-item href="#">Sign Out</b-dropdown-item>-->
          <!--          </b-nav-item-dropdown>-->
          <!--        </b-navbar-nav>-->
        </b-collapse>
      </b-container>

    </b-navbar>


  </header>

</template>

<script>
import AppLogo from "@/components/AppLogo";

export default {
  name: 'AppHeader',
  components: {AppLogo},
  data() {
    return {
      scrollPosition: null,
      number: .9,
      numberReverse: 1
    }
  },
  mounted() {
    window.addEventListener('scroll', this.updateScroll);
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.updateScroll)
  },
  methods: {
    updateScroll() {
      this.scrollPosition = window.scrollY;
      this.number = this.scrollPosition <= 300 ? this.scrollPosition / 300 : 1;

      this.numberReverse = this.scrollPosition <= 300 ? 1 - this.scrollPosition / 300 : .9;
    },
  }
}
</script>

<style lang="scss" scoped>
#header {
  padding: 0;
}

.navbar {
  transition: .3s;
  background: rgba(118, 112, 180, 1);
}
.navbar-brand {
  position: relative;
  left: 0;

  @media (max-width: 992px) {
    margin-left: 15px;
  }
}

.navbar-light {
  .navbar-nav {
    .nav-link {
      padding: .5rem 1rem;
      border-radius: 50px;
      color: rgba(255, 255, 255, 0.75);

      &:hover {
        background: rgba(0, 0, 0, 0.05);
      }
      a {
        text-decoration: none;
      }
    }
  }

  .navbar-text {
    a {
      color: rgba(255, 255, 255, 0.75);
    }
  }
}

.navbar-toggler {
  position: relative;
  right: 20px;
  width: 50px;
  height: 50px;
  border: 0;
  text-align: center;
  padding: 0;
  color: #ffffff;
}

#nav-collapse {
  border-radius: 10px;

  @media (max-width: 991px) {
    margin: 1rem 0 0;
    padding: .5rem 1rem;
  }

  @media (min-width: 992px) {
    background: none !important;
  }
}

/* NINE */

.hamburger {

  .line {
    width: 35px;
    height: 2px;
    background-color: rgba(255, 255, 255, 0.75);
    display: block;
    margin: 8px auto;
    transition: all 0.3s ease-in-out;
  }

  &.is-active {
    .line {
      height: 2px;
      background-color: rgba(255, 255, 255, 0.5);
    }
  }
}

#hamburger-9{
  position: relative;
  transition: all 0.3s ease-in-out;
}

#hamburger-9.is-active{
  transform: rotate(45deg);
}

#hamburger-9:before{
  content: "";
  position: absolute;
  box-sizing: border-box;
  width: 40px;
  height: 40px;
  border: 2px solid transparent;
  top: calc(50% - 20px);
  left: calc(50% - 20px);
  border-radius: 100%;
  transition: all 0.3s ease-in-out;
}

#hamburger-9.is-active:before{
  border: 4px solid rgba(255, 255, 255, 0.5);
}

#hamburger-9.is-active .line{
  width: 35px;
}

#hamburger-9.is-active .line:nth-child(2){
  opacity: 0;
}

#hamburger-9.is-active .line:nth-child(1){
  transform: translateY(10px);
}

#hamburger-9.is-active .line:nth-child(3){
  transform: translateY(-10px) rotate(90deg);
}
</style>
