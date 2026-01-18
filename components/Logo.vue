<template>
  <div
    class="tw-fixed tw-top-0 tw-left-0 tw-right-0 tw-z-50 tw-flex tw-justify-center tw-w-full tw-transition-all tw-duration-300"
    :class="navClass"
  >
    <div class="tw-flex tw-justify-between tw-items-center stable-alignment tw-w-full">
      <!-- Logo -->
      <p
        class="title tw-cursor-pointer tw-group"
        :class="color"
        @click.prevent="$router.push({ path: '/' })"
      >
        Obadoni
        <span class="tw-text-complimentry group-hover:tw-text-primary">.</span>
      </p>

      <!-- Mobile Menu Icon -->
      <i
        @click.prevent="isVisible = true"
        class="bx bx-menu tw-text-3xl md:tw-text-5xl md:tw-bg-black tw-p-3 tw-rounded-full tw-text-complimentry hover:tw-text-compgreen tw-cursor-pointer"
      ></i>
    </div>

    <!-- Mobile Menu -->
    <div
      v-if="isVisible"
      data-aos="fade-down"
      class="tw-fixed menu-bg tw-top-0 tw-bottom-0 tw-left-0 tw-right-0 tw-z-50"
    >
      <div class="stable-alignment tw-h-full tw-py-8 md:tw-py-16 tw-flex tw-flex-col tw-justify-between">

        <!-- Menu Header -->
        <div class="tw-flex tw-justify-between tw-items-center">
          <p
            class="title tw-text-white tw-cursor-pointer"
            @click.prevent="$router.push({ path: '/' })"
          >
            Obadoni <span class="tw-text-complimentry">.</span>
          </p>

          <i
            @click.prevent="isVisible = false"
            class="bx bx-x tw-text-3xl md:tw-text-5xl md:tw-bg-black tw-p-3 tw-rounded-full tw-text-complimentry hover:tw-text-compgreen tw-cursor-pointer"
          ></i>
        </div>

        <!-- Menu Links -->
        <div class="tw-space-y-8">
          <nuxt-link
            @click.native="setActiveMenu"
            to="/"
            exact
            class="tw-text-3xl tw-text-white tw-flex tw-items-center tw-cursor-pointer hover:tw-text-primary hover:tw-font-semibold"
          >
            Home
          </nuxt-link>

          <nuxt-link
            @click.native="setActiveMenu"
            to="/about"
            exact
            class="tw-text-3xl tw-text-white tw-flex tw-items-center tw-cursor-pointer hover:tw-text-primary hover:tw-font-semibold"
          >
            About Me
          </nuxt-link>

          <nuxt-link
            @click.native="setActiveMenu"
            to="/projects"
            exact
            class="tw-text-3xl tw-text-white tw-flex tw-items-center tw-cursor-pointer hover:tw-text-primary hover:tw-font-semibold"
          >
            Projects
          </nuxt-link>

          <nuxt-link
            @click.native="setActiveMenu"
            to="/technologies"
            exact
            class="tw-text-3xl tw-text-white tw-flex tw-items-center tw-cursor-pointer hover:tw-text-primary hover:tw-font-semibold"
          >
            Technologies
          </nuxt-link>

          <nuxt-link
            @click.native="setActiveMenu"
            to="/hire"
            exact
            class="tw-text-3xl tw-text-white tw-flex tw-items-center tw-cursor-pointer hover:tw-text-primary hover:tw-font-semibold"
          >
            Contact
          </nuxt-link>

          <Social />
        </div>

        <div></div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import aosMixin from "~/plugins/aos";

export default Vue.extend({
  props: {
    color: {
      type: String,
      default: "tw-text-white",
    },
  },

  data() {
    return {
      isVisible: false,
      isSticky: false,
    };
  },

  mixins: [aosMixin],

  computed: {
    navClass() {
      return this.isSticky
        ? "tw-bg-secondary tw-blur-3xl tw-py-3 md:tw-py-4"
        : "tw-py-4 md:tw-py-16";
    },
  },

  methods: {
    handleScroll() {
      this.isSticky = window.pageYOffset > 20;
    },

    setMouse() {
      const cursor: any = document.querySelector(".cursor");

      document.addEventListener("mousemove", (e) => {
        cursor.style.left = e.clientX + "px";
        cursor.style.top = e.clientY + "px";
      });

      const elements = document.querySelectorAll("h1, h2, h3, h4, h5, h6, p, i, span, img");

      elements.forEach((el) => {
        el.addEventListener("mouseover", () => (cursor.style.transform = "scale(10)"));
        el.addEventListener("mouseout", () => (cursor.style.transform = "scale(1)"));
      });
    },

    setActiveMenu() {
      this.isVisible = false;
    },
  },

  mounted() {
    this.setMouse();
    window.addEventListener("scroll", this.handleScroll);
  },

  beforeDestroy() {
    window.removeEventListener("scroll", this.handleScroll);
  },
});
</script>

<style lang="scss">
.menu-bg {
  background: linear-gradient(45deg, theme("colors.secondary2"), #1d1d1d);
  background-size: cover;
  background-repeat: no-repeat;
  background-blend-mode: difference;
}

a.nuxt-link-active {
  font-weight: bold;
  color: theme("colors.primary");
  text-decoration: line-through solid theme("colors.complimentry") 5%;
}
</style>
