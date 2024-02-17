<template>

  <header
    id="header"
    ref="header"
  >

    <b-navbar
        toggleable="lg"
        fixed="top"
        :style="[{background: `rgba(0,0,0,${number}`}, {padding: `${scrollPosition > 80 ? '0' : '15px'} 0`}]"
    >
      <b-container fluid="xl" class="justify-content-between">
        <b-navbar-brand href="/">
          <app-logo :height="scrollPosition > 80 ? 54 : 60" />

        </b-navbar-brand>

        <b-navbar-toggle target="nav-collapse">
<!--          <b-icon-list />-->
        </b-navbar-toggle>

        <b-collapse id="nav-collapse" class="justify-content-end" is-nav :style="{background: `rgba(0,0,0,${numberReverse}`}">
          <b-navbar-nav class="ml-auto">

            <b-nav-item class="nav-link scrollto active" href="#hero">Home</b-nav-item>
            <b-nav-item class="nav-link scrollto" href="#about">About</b-nav-item>

            <div
              v-if="$route.name === 'index'"
              class="search d-flex align-center justify-end ml-3"
            >
              <b-input-group size="sm" class="align-items-center">
<!--                <template #prepend>-->
<!--                  <b-input-group-text><b-icon icon="search"></b-icon></b-input-group-text>-->
<!--                </template>-->
                <b-form-input
                  v-model="search"
                  type="search"
                  hide-details="auto"
                  placeholder="Search for a post"
                  @click:append="clearSearch"
                />
              </b-input-group>


            </div>

          </b-navbar-nav>

          <!--        <b-navbar-nav class="ml-auto">-->


          <!--          <b-nav-item-dropdown text="Lang" right>-->
          <!--            <b-dropdown-item href="#">EN</b-dropdown-item>-->
          <!--            <b-dropdown-item href="#">ES</b-dropdown-item>-->
          <!--            <b-dropdown-item href="#">RU</b-dropdown-item>-->
          <!--            <b-dropdown-item href="#">FA</b-dropdown-item>-->
          <!--          </b-nav-item-dropdown>-->

          <!--          <b-nav-item-dropdown right>-->
          <!--            &lt;!&ndash; Using 'button-content' slot &ndash;&gt;-->
          <!--            <template #button-content>-->
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
      number: 0,
      numberReverse: 1
    }
  },
  computed: {
    search: {
      get() {
        return this.$store.state.query
      },
      set(value) {
        this.$store.commit('SET_QUERY', value)
      },
    },
  },
  mounted() {
    window.addEventListener('scroll', this.updateScroll);
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.updateScroll)
  },
  methods: {
    clearSearch() {
      this.$store.commit('SET_QUERY', '')
    },
    updateScroll() {
      this.scrollPosition = window.scrollY;
      this.number = this.scrollPosition <= 300 ? this.scrollPosition / 300 : 1;

      this.numberReverse = this.scrollPosition <= 300 ? 1 - this.scrollPosition / 300 : 0;
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
}
.navbar-brand {
  position: relative;
  left: 0;
}

.nav-link {
  color: #ffffff !important;
}

.nav-link:hover, .nav-link:focus {
  color: $pink !important;
}

.navbar-toggler {
  border: 0;
  padding: .5rem;
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
</style>
